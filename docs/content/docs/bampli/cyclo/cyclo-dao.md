---
title: Data Access
weight: 40
---
# Data Access

## SessionManager

### Methods

```python
- get_instance()
- save_credentials(self, username, password, keyspace, scbpath)
- test_credentials(self, username, password, keyspace, scbpath)
- connect(self)
- check_connection(self)
- close(self)
```

## CycloJourneyCatalogDAO

### Methods
```python
- maybe_create_schema(self)
- write_journey(self, cyclo_name, journey_id, start, end, active, summary)
- get_all_journeys(self)
- get_all_journeys_for_cyclo(self, cyclo_name)
- get_single_journey_for_cyclo(self, cyclo_name, journey_id)
```
## CycloSpinDAO

### Methods
```python
- maybe_create_schema(self)
- write_readings(self, cyclo_name, stage_name, journey_id, data)
- get_spin_readings_for_cyclo_journey(self, cyclo_name, journey_id,
                                      page_size=25, page_state=None)
```