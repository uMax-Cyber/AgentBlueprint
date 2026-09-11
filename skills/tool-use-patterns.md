# Tool-Use Patterns — 11 Call Recipes

## Pattern 1: Site/Resource ID Resolution
Before calling any tool that requires a site_id/resource_id:
```python
# Step 1: Get the list
sites = call_tool("list_sites")
# Step 2: Extract the ID
site_id = sites[0]["id"]  # from the RESULT, not from memory
# Step 3: Use it
devices = call_tool("list_devices", site_id=site_id)
```

## Pattern 2: Routed-Tool Sequence
For servers with tool routing:
```
route_tools(query="what you want") → get tool names
call_routed_tool(name=from_result, arguments={...})
```
Never call raw API endpoints when a routed tool exists.

## Pattern 3: Error → Alternative (not Error → Imagination)
```
tool_call_1 → ERROR "not enabled"
↓
tool_call_2 (different approach) → SUCCESS
↓
answer from tool_call_2 results
```

## Pattern 4: Anti-Wandering (Stop When Done)
Once you have the data needed to answer, STOP calling tools.
Every call after you COULD have answered is wasted time and risk.

## Pattern 5: Lifecycle (create→verify→delete)
For test entities:
```
create(entity) → list(to get ID from result) → delete(ID from list)
```
IDs only from tool results. Verify cleanup after.

## Pattern 6: Multi-Instance Routing
If you have multiple servers (gw1, gw2, node1, node2):
- Question about gateway 1 → use gateway-1 tools
- "Both/all" → call ALL instances separately, label results

## Pattern 7: Focus Discipline
Question about node-A → answer contains ONLY node-A data.
Mentioning node-B/node-C = failure, regardless of data correctness.
