# AI Agent Integration Guide for The Best Sort

This document provides guidance for AI systems, language models, and automated agents integrating with The Best Sort framework.

## Project Overview

**Project Name**: The Best Sort
**Purpose**: framework demonstrating async visualization and design patterns
**Language**: TypeScript
**Type**: Sorting library using setTimeout-based strategies

## Core Architecture

### Key Components

```
src/index.ts
├── Interfaces & Types (IComparable, IObserver, IStrategy, etc.)
├── Singleton: ConfigurationManager
├── Observable: VisualizationContext
├── Observers: ConsoleLoggingObserver, StatisticsObserver, HistoryObserver
├── Strategy: TimeoutForEachStrategy
├── Factory: ConcreteVisualizationStrategyFactory
├── Builder: VisualizerBuilder
├── Facade: ArrayVisualizer
├── Command: ExecuteVisualizationCommand, CommandInvoker
├── Template Method: AbstractVisualizationRunner
└── Main: demonstrateVisualization()
```


## Main Classes and Their Responsibilities

### ConfigurationManager (Singleton)
- **Purpose**: Global configuration management
- **Methods**: `getInstance()`, `getConfig()`, `updateConfig()`, `resetToDefaults()`
- **Key Properties**: baseDelayMs, enableLogging, logPrefix, showTimestamps, colorize
- **Usage**: Should be used to configure all framework behavior

### VisualizationContext (Subject/Observable)
- **Purpose**: Core event system and state management
- **Key Methods**: 
  - `attach(observer)` - Add observer
  - `detach(observer)` - Remove observer
  - `emitStarted()` - Signal visualization start
  - `emitElementDisplayed(element, index, delay)` - Signal element display
  - `emitCompleted()` - Signal completion
  - `emitError(error)` - Signal error
- **Events**: STARTED, ELEMENT_DISPLAYED, COMPLETED, ERROR

### Observers

#### ConsoleLoggingObserver
- **Purpose**: Log events to console with formatting
- **Usage**: Add for human-readable output
- **Respects**: Configuration settings (enableLogging, logPrefix, showTimestamps)

#### StatisticsObserver
- **Purpose**: Collect performance metrics
- **Metrics**: duration, displayedElements, totalDelay, averageDelay, eventCounts
- **Methods**: `getStatistics()`, `printStatistics()`, `reset()`
- **Use Case**: Performance analysis and monitoring

#### HistoryObserver
- **Purpose**: Record complete event history
- **Methods**: `getHistory()`, `printHistory()`, `clear()`
- **Use Case**: Debugging and auditing visualization execution

### ArrayVisualizer (Facade)
- **Purpose**: Main interface for users and agents
- **Key Methods**:
  - `execute()` - Run visualization
  - `addObserver(observer)` - Subscribe to events
  - `removeObserver(observer)` - Unsubscribe
  - `getContext()` - Access underlying context
  - `getEventHistory()` - Get all events
- **Properties**: array, strategy

### VisualizerBuilder (Builder Pattern)
- **Purpose**: Fluent interface for constructing visualizers
- **Methods**: `setArray()`, `setStrategy()`, `addObserver()`, `setConfig()`, `build()`, `reset()`
- **Chainable**: All setters return `this` for chaining
- **Example**: 

```typescript
new VisualizerBuilder<T>()
  .setArray(array)
  .setStrategy(strategy)
  .addObserver(observer)
  .build()
```


### TimeoutForEachStrategy
- **Purpose**: Core visualization strategy
- **Implementation**: Uses `arr.forEach((t) => setTimeout(() => console.log(t), t))`
- **Behavior**: Each element displays after delay equal to its numeric value
- **Methods**: `visualize()`, `getName()`, `getDescription()`

### ConcreteVisualizationStrategyFactory (Factory Pattern)
- **Purpose**: Create strategy instances
- **Methods**: `createStrategy(type)`, `registerStrategy(type, strategy)`, `listAvailableStrategies()`
- **Caching**: Caches created strategies
- **Current Strategies**: TIMEOUT_FOREACH

### CommandInvoker (Command Pattern)
- **Purpose**: Queue and execute commands
- **Methods**: `enqueueCommand()`, `executeNext()`, `executeAll()`, `getQueueSize()`, `clearQueue()`
- **Use Case**: Deferred execution, undo/redo patterns

### AbstractVisualizationRunner (Template Method)
- **Purpose**: Customizable execution flow
- **Methods**: `run(array, strategyType)`
- **Override Points**: `beforeRun()`, `afterRun()`, `buildVisualizer()`, `executeVisualization()`
- **Subclass**: LoggingVisualizationRunner

## Design Patterns Used

| Pattern | Class | Purpose |
|---------|-------|---------|
| Singleton | ConfigurationManager | Global state management |
| Factory | ConcreteVisualizationStrategyFactory | Create strategies |
| Builder | VisualizerBuilder | Fluent construction |
| Facade | ArrayVisualizer | Simplified interface |
| Strategy | IVisualizationStrategy | Interchangeable algorithms |
| Observer | IObserver + VisualizationContext | Event notifications |
| Command | CommandInvoker | Deferred execution |
| Template Method | AbstractVisualizationRunner | Customizable flow |
| Decorator | @Measure, @Log, @ValidateArray | Method enhancement |

## Data Structures

### VisualizableNumber

```typescript
{
  value: number // The numeric value
}
```


### VisualizationEvent<T>

```typescript
{
  type: EventType, // STARTED | ELEMENT_DISPLAYED | COMPLETED | ERROR
  element?: T, // The affected element
  index?: number, // Array index
  timestamp: number, // Unix timestamp
  delay?: number, // Delay in milliseconds
  metadata?: Record<string, any>
}
```


### VisualizationConfig

```typescript
{
  baseDelayMs: number, // Delay multiplier
  enableLogging: boolean, // Log to console
  logPrefix: string, // Log message prefix
  showTimestamps: boolean, // Include timestamps
  colorize: boolean // Colorize output
}
```

## Typical Workflow for Agents

### Basic Usage Pattern

1. Create VisualizableNumber array

2. Get strategy from factory

3. Create observer(s)

4. Build visualizer with VisualizerBuilder

5. Call visualizer.execute()

6. Wait for completion (set timeout)

7. Retrieve metrics from observers

8. Analyze results


### Advanced Usage Pattern

1. Configure globally via ConfigurationManager

2. Create multiple observers for different purposes

3. Build custom runner extending AbstractVisualizationRunner

4. Use CommandInvoker to queue multiple visualizations

5. Execute commands in sequence or parallel (with care)

6. Aggregate metrics from all observers

7. Generate reports


## Important Technical Details

### Asynchronous Execution

All visualization is asynchronous via setTimeout. Key points:
- Events emit after their respective delays
- COMPLETED event fires AFTER all elements display
- Use setTimeout/Promise to wait for completion
- Event history available immediately after execute() call
- Metrics only finalized after visualization completes

### Event Flow

```
execute() called
↓
STARTED event
↓
setTimeout schedules for each element
↓
On delay expiration: ELEMENT_DISPLAYED event
↓
After all elements: COMPLETED event
```


### Observer Notification

- Observers notified synchronously when event emitted
- Events can occur at different times (async)
- Multiple observers can be attached
- Observer order not guaranteed

## Integration Examples

### Monitoring Integration

```typescript
const monitor = new StatisticsObserver<VisualizableNumber>();
const visualizer = new VisualizerBuilder<VisualizableNumber>()
  .setArray(array)
  .setStrategy(strategy)
  .addObserver(monitor)
  .build();

visualizer.execute();

setTimeout(() => {
  const stats = monitor.getStatistics();
  console.log(`Completed in ${stats.duration}ms`);
}, 5000);
```


### History Tracking

```typescript
const history = new HistoryObserver<VisualizableNumber>();
visualizer.addObserver(history);
visualizer.execute();

setTimeout(() => {
  const events = history.getHistory();
  events.forEach(e => console.log(e.event.type));
}, 5000);
```

### Custom Configuration

```typescript
ConfigurationManager.getInstance().updateConfig({
  baseDelayMs: 500,
  enableLogging: false
});
```

## Extension Points for Agents

### Add Custom Strategy

1. Extend `AbstractVisualizationStrategy<T>`
2. Implement: `visualize()`, `getName()`, `getDescription()`
3. Register with factory: `factory.registerStrategy(type, newStrategy)`

### Add Custom Observer

1. Implement `IObserver<T>`
2. Implement: `update(event: VisualizationEvent<T>)`
3. Add to visualizer: `visualizer.addObserver(observer)`

### Add Custom Runner

1. Extend `AbstractVisualizationRunner<T>`
2. Override: `beforeRun()`, `afterRun()`, `buildVisualizer()`, `executeVisualization()`
3. Call: `runner.run(array, strategyType)`

## File Structure for Agents

- **Main File**: `src/index.ts` - All implementation
- **Config**: `tsconfig.json` - TypeScript configuration
- **Package**: `package.json` - Dependencies and scripts
- **Documentation**: `README.md`, `CONTRIBUTING.md`, `SECURITY.md`, `CHANGELOG.md`

## Recommended Setup for Agent Processing

```typescript
// 1. Configure
ConfigurationManager.getInstance().updateConfig({
  enableLogging: false, // Disable console output
  baseDelayMs: 1000 // Set appropriate delay
});

// 2. Create observers
const stats = new StatisticsObserver<VisualizableNumber>();
const history = new HistoryObserver<VisualizableNumber>();

// 3. Build visualizer
const visualizer = new VisualizerBuilder<VisualizableNumber>()
  .setArray(array)
  .setStrategy(strategy)
  .addObserver(stats)
  .addObserver(history)
  .disableDefaultObservers() // Disable console logging
  .build();

// 4. Execute
visualizer.execute();

// 5. Wait and analyze
setTimeout(() => {
  const metrics = stats.getStatistics();
  const events = history.getHistory();
  // Process results
}, 5000);
```

---

For detailed architecture information, see README.md and CONTRIBUTING.md.

