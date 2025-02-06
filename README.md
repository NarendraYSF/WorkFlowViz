# WorkflowViz.js

A lightweight JavaScript library for creating interactive workflow visualizations. Transform your task management data into beautiful, interactive flowcharts with minimal setup.

## Features

- Drag-and-drop workflow builder
- Real-time status updates
- Customizable node styles and transitions
- Built-in templates for common workflow patterns
- Export/import functionality
- Mobile-responsive design
- Zero dependencies

## Installation

```bash
npm install workflow-viz
# or
yarn add workflow-viz
```

## Quick Start

```javascript
import WorkflowViz from 'workflow-viz';

// Initialize with a container element
const workflow = new WorkflowViz('#workflow-container');
```

## Simple Usage Examples

### 1. Create a Single Workflow Line

```javascript
<div id="simple-workflow"></div>

<script>
  // Define workflow steps with timestamps and status
  var line = {
    name: "Project Alpha",
    data: [
      [1707235200000, "Planning"],     // Feb 6, 2024
      [1707321600000, "Development"],   // Feb 7, 2024
      [1707408000000, "Testing"]        // Feb 8, 2024
    ]
  };

  // Add important milestones or events
  var markers = [
    [1707321600000, "Development Sprint Started"],
    [1707408000000, "QA Review Completed"]
  ];

  $('#simple-workflow').workflowviz(line, markers);
</script>
```

### 2. Create Multiple Workflow Lines

```javascript
<div id="multi-workflow"></div>

<script>
  // Define multiple workflow streams
  var frontend = {
    name: "Frontend Development",
    data: [
      [1707235200000, "Design"],
      [1707321600000, "Implementation"],
      [1707408000000, "Testing"]
    ]
  };

  var backend = {
    name: "Backend Development",
    data: [
      [1707235200000, "Architecture"],
      [1707321600000, "API Development"],
      [1707408000000, "Integration"]
    ]
  };

  var lines = [frontend, backend];
  
  // Add shared milestones
  var markers = [
    [1707321600000, "Sprint 1 Review"],
    [1707408000000, "Integration Complete"]
  ];

  $('#multi-workflow').workflowviz(lines, markers);
</script>
```

### 3. Customize Workflow Visualization

```javascript
<div id="custom-workflow"></div>

<script>
  var line = {
    name: "Release Pipeline",
    data: [
      [1707235200000, "Development"],
      [1707321600000, "Testing"],
      [1707408000000, "Deployment"]
    ]
  };

  var markers = [
    [1707408000000, "Production Release"]
  ];

  // Custom options
  var options = {
    theme: 'dark',
    nodeStyle: {
      shape: 'rectangle',
      color: '#4A90E2'
    },
    markerStyle: {
      icon: 'flag',
      color: '#E24A90'
    },
    dateFormat: 'MMM DD, YYYY'
  };

  $('#custom-workflow').workflowviz(line, markers, options);
</script>
```

## Advanced Usage

### Custom Node Templates

```javascript
workflow.defineTemplate('custom', {
    shape: 'hexagon',
    size: { width: 120, height: 80 },
    style: {
        fill: '#e6f3ff',
        stroke: '#0066cc',
        textColor: '#333333'
    }
});

workflow.addNode({
    id: 'special-task',
    label: 'Custom Process',
    template: 'custom'
});
```

### Event Handling

```javascript
workflow.on('nodeClick', (node) => {
    console.log(`Node ${node.id} clicked`);
});

workflow.on('connectionCreated', (source, target) => {
    console.log(`New connection: ${source} → ${target}`);
});
```

### State Management

```javascript
// Update node status
workflow.updateNode('task1', {
    status: 'completed',
    metadata: {
        completedBy: 'John Doe',
        timestamp: Date.now()
    }
});

// Get workflow state
const state = workflow.exportState();
```

## Configuration Options

```javascript
const config = {
    theme: 'light',           // 'light' or 'dark'
    autoLayout: true,         // Enable automatic node positioning
    gridSize: 20,            // Snap-to-grid size in pixels
    animationDuration: 300,   // Transition duration in milliseconds
    readonly: false,         // Disable editing capabilities
    connectorStyle: 'curved' // 'straight', 'curved', or 'orthogonal'
};

const workflow = new WorkflowViz('#container', config);
```

## API Reference

### Core Methods

- `addNode(config)`: Add a new node to the workflow
- `removeNode(id)`: Remove a node by ID
- `connect(sourceId, targetId)`: Create a connection between nodes
- `disconnect(sourceId, targetId)`: Remove a connection
- `clear()`: Remove all nodes and connections
- `exportState()`: Export the current workflow state
- `importState(state)`: Import a workflow state
- `render()`: Update the visualization

### Events

- `nodeClick`: Fired when a node is clicked
- `nodeDragStart`: Fired when node dragging begins
- `nodeDragEnd`: Fired when node dragging ends
- `connectionCreated`: Fired when a new connection is created
- `connectionRemoved`: Fired when a connection is removed
- `stateChanged`: Fired when the workflow state changes

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- IE11 (with polyfills)

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

## License

MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- Documentation: [docs.workflowviz.js.org](https://docs.workflowviz.js.org)
- Issues: [GitHub Issues](https://github.com/workflowviz/workflowviz/issues)
- Discord: [Join our community](https://discord.gg/workflowviz)

## Credits

Created and maintained by the WorkflowViz team. Special thanks to all our contributors!
