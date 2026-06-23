---
name: no-use-effect
description: >-
  Enforce the no-useEffect rule when writing or reviewing React code.
  ACTIVATE when writing React components, refactoring existing useEffect calls,
  reviewing PRs with useEffect, or when an agent adds useEffect "just in case."
  Provides the five replacement patterns and the useMountEffect escape hatch.
---

# No useEffect

Never call `useEffect` directly in a component. Use derived state, event handlers, TanStack data primitives, `useSyncExternalStore`, callback refs, or `useMountEffect` instead.

For TanStack Start and TanStack Query code:

- Never fetch server data inside `useEffect`
- Prefer route loaders for route-level data
- Prefer `useQuery`, `useSuspenseQuery`, and `useMutation`
- Prefer `queryClient.prefetchQuery` and `invalidateQueries`
- Avoid manual loading/error state when TanStack Query can own server state

## Quick Reference

- Lint rule: `no-restricted-syntax` (configured to ban `useEffect`)
- React docs: [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)
- Origin: [https://x.com/alvinsng/status/2033969062834045089](https://x.com/alvinsng/status/2033969062834045089)

| Instead of useEffect for... | Use |
| --- | --- |
| Deriving state from other state/props | Inline computation or `useMemo` (Rule 1) |
| Fetching server data | Route loaders, `useQuery`, `useSuspenseQuery`, `useMutation` (Rule 2) |
| Responding to user actions | Event handlers (Rule 3) |
| One-time external sync on mount | `useMountEffect` (Rule 4) |
| Resetting state when a prop changes | `key` prop on parent (Rule 5) |
| External store subscriptions | `useSyncExternalStore` |
| DOM node setup/measurement | Callback refs |

## When to Use This Skill

- Writing new React components
- Refactoring existing `useEffect` calls
- Reviewing PRs that introduce `useEffect`
- An agent adds `useEffect` "just in case"

## Workflow

### 1. Identify the Real Problem

Before writing an effect, ask: what am I actually trying to do?

- Compute a value from props or state
- Respond to a user event
- Fetch or mutate server data
- Subscribe to an external store
- Integrate with the DOM or a third-party API
- Reset component state for a new entity

If the answer is not "synchronize this component with an external system," you almost certainly do not need an effect.

### 2. Run the Smell Check

Stop and rewrite if the effect is doing any of these:

- Derived state: `setX(f(y))`
- Copying props into state
- Filtered, sorted, mapped, or aggregated state
- Event-driven logic hidden behind state flags
- Fetching data and then `setState`
- Manual loading/error state for server data
- Synchronizing one piece of React state to another piece of React state
- Dependency-array workarounds
- Stale-closure workarounds
- Refs used only to silence `exhaustive-deps`
- Ref guards like `hasRun.current` or `isMounted.current`

### 3. Apply the Correct Replacement Pattern

Use the five rules below to pick the right replacement.

### 4. Verify

```
npm run lint -- --filter=<package>
npm run typecheck -- --filter=<package>
npm run test -- --filter=<package>
```

## The Escape Hatch: useMountEffect

For the rare case where you need to sync with an external system on mount:

The implementation wraps `useEffect` with an empty dependency array to make intent explicit:

```tsx
export function useMountEffect(effect: () => void | (() => void)) {
  /* eslint-disable no-restricted-syntax */
  useEffect(effect, []);
}
```

Direct `useEffect` may still exist inside a reusable custom hook when there is no better primitive, but components must never import or call it directly.

## Replacement Patterns

### Rule 1: Derive state, do not sync it

Most effects that set state from other state are unnecessary and add extra renders.

```tsx
// BAD: Two render cycles - first stale, then filtered
function ProductList() {
  const [products, setProducts] = useState([]);
  const [filteredProducts, setFilteredProducts] = useState([]);

  useEffect(() => {
    setFilteredProducts(products.filter((p) => p.inStock));
  }, [products]);
}

// GOOD: Compute inline in one render
function ProductList() {
  const [products, setProducts] = useState([]);
  const filteredProducts = products.filter((p) => p.inStock);
}
```

For expensive calculations, use `useMemo` instead of effect-driven state:

```tsx
const visibleTodos = useMemo(
  () => getFilteredTodos(todos, filter),
  [todos, filter]
);
```

**Smell test:** You are about to write `useEffect(() => setX(deriveFromY(y)), [y])`, or you have state that only mirrors props, state, filtered lists, sorted lists, mapped data, totals, or selections that can be computed during render.

### Rule 2: Use data-fetching libraries

Effect-based fetching creates race conditions and duplicated caching logic.

```tsx
// BAD: Race condition risk
function ProductPage({ productId }) {
  const [product, setProduct] = useState(null);

  useEffect(() => {
    fetchProduct(productId).then(setProduct);
  }, [productId]);
}

// GOOD: Query library handles cancellation/caching/staleness
function ProductPage({ productId }) {
  const { data: product } = useQuery(['product', productId], () =>
    fetchProduct(productId)
  );
}
```

In TanStack apps:

- Route-level data belongs in loaders
- Component-level server state belongs in `useQuery` or `useSuspenseQuery`
- Writes belong in `useMutation`
- Warm caches with `queryClient.prefetchQuery`
- Refresh views with `invalidateQueries`

Never fetch server data in a component effect. Do not hand-roll caching, retries, cancellation, deduplication, stale handling, loading flags, or error flags when TanStack Query already owns that problem.

**Smell test:** Your effect does `fetch(...)` and then `setState(...)`, or you are manually managing `isLoading`, `error`, retries, cancellation, or stale data for server state.

### Rule 3: Event handlers, not effects

If a user clicks a button, submits a form, or changes a control, do the work in the handler.

```tsx
// BAD: Effect as an action relay
function LikeButton() {
  const [liked, setLiked] = useState(false);

  useEffect(() => {
    if (liked) {
      postLike();
      setLiked(false);
    }
  }, [liked]);

  return <button onClick={() => setLiked(true)}>Like</button>;
}

// GOOD: Direct event-driven action
function LikeButton() {
  return <button onClick={() => postLike()}>Like</button>;
}
```

Parent notifications also belong in the same event path, not in an effect:

```tsx
function updateToggle(nextIsOn) {
  setIsOn(nextIsOn);
  onChange(nextIsOn);
}
```

**Smell test:** State is used as a flag so an effect can do the real action, or you are building "set flag -> effect runs -> reset flag" mechanics, form submission relays, analytics relays, or React-state-to-React-state synchronization.

### Rule 4: useMountEffect for one-time external sync

Good uses: DOM integration, focus, scroll, third-party widget lifecycles, and browser API subscriptions that naturally mean "setup on mount, cleanup on unmount."

```tsx
// BAD: Guard inside effect
function VideoPlayer({ isLoading }) {
  useEffect(() => {
    if (!isLoading) playVideo();
  }, [isLoading]);
}

// GOOD: Mount only when preconditions are met
function VideoPlayerWrapper({ isLoading }) {
  if (isLoading) return <LoadingScreen />;
  return <VideoPlayer />;
}

function VideoPlayer() {
  useMountEffect(() => playVideo());
}
```

Prefer a more specific primitive when available:

- `useSyncExternalStore` for external store subscriptions
- Callback refs for DOM node measurement, focus, and setup

**Smell test:** You are synchronizing with an external system, and the behavior is naturally "setup on mount, cleanup on unmount." If you need a ref just to make the effect stop looping or stop the linter from complaining, the effect is wrong.

### Rule 5: Reset with key, not dependency choreography

```tsx
// BAD: Effect attempts to emulate remount behavior
function VideoPlayer({ videoId }) {
  useEffect(() => {
    loadVideo(videoId);
  }, [videoId]);
}

// GOOD: key forces clean remount
function VideoPlayer({ videoId }) {
  useMountEffect(() => {
    loadVideo(videoId);
  });
}

function VideoPlayerWrapper({ videoId }) {
  return <VideoPlayer key={videoId} videoId={videoId} />;
}
```

This also applies to forms, selections, wizard steps, and any state that should start fresh for a new entity.

**Smell test:** You are writing an effect whose only job is to clear, reload, or reset local state when an ID or prop changes, or you want the component to behave like a brand-new instance for each entity.

## Component Structure Convention

Computed values come after hooks and local state, never via `useEffect`:

```tsx
export function FeatureComponent({ featureId }: ComponentProps) {
  // Hooks first
  const { data, isLoading } = useQueryFeature(featureId);

  // Local state
  const [isOpen, setIsOpen] = useState(false);

  // Computed values (NOT useEffect + setState)
  const displayName = user?.name ?? 'Unknown';

  // Event handlers
  const handleClick = () => {
    setIsOpen(true);
  };

  // Early returns
  if (isLoading) return <Loading />;

  // Render
  return <Flex direction="column" gap="lg">...</Flex>;
}
```
