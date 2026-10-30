# Navigate Through Poses — Nav2 waypoint skill

This project was previously known as AgenticROS.


Marketplace package for the `navigate_through_poses` capability (`external_ros_node` → Nav2 `NavigateThroughPoses`).

```bash
npx @corebrum/synapse skills install @corebrum/navigate-through-poses
# or marketplace ref: chrismatthieu/navigate-through-poses
# or: "skillRefs": ["chrismatthieu/navigate-through-poses"]
```

Corebrum Synapse does **not** launch Nav2. Bring up Nav2 on the robot (or sim), then install this skill. The CLI auto-restarts the OpenClaw gateway unless you pass `--no-restart`.

## Mission example

```json
{
  "mission": {
    "name": "patrol loop",
    "steps": [
      {
        "id": "patrol",
        "capability": "navigate_through_poses",
        "inputs": {
          "poses": [
            { "x": 1.0, "y": 0.0, "yaw": 0 },
            { "x": 1.0, "y": 2.0, "yaw": 1.57 },
            { "x": 0.0, "y": 0.0, "yaw": 3.14 }
          ]
        },
        "retry": { "max_attempts": 2, "backoff_ms": 500 }
      }
    ]
  }
}
```

Or pass an explicit Nav2 goal: `{ "goal": { "poses": [ ... ] } }`.

## Requirements

- Nav2 advertising `navigate_through_poses` (namespaced under the robot namespace when applicable)
- Transport that supports actions (local DDS, rosbridge, or WebRTC)
- `@corebrum/core` ≥ 0.8.1 for the `poses[]` → goal helper (explicit `goal` works on older cores)
