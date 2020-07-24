---
title: Service
weight: 30
---
# Service

## CycloService

### Properties

```python
- cyclo_journey_catalog_dao
- cyclo_spin_dao
- _session_manager = SessionManager()
- _session
```
### Methods

```python
- get_session(self)
- save_credentials(self, username, password, keyspace, scbpath)
- test_credentials(self, username, password, keyspace, scbpath)
- connect(self)
- check_connection(self)
- get_cyclo_journey_catalog_dao(self)
- get_cyclo_spin_dao(self)
- create_new_journey_for_cyclo(self, cyclo_name, journey_id,
                               start, end, active, summary)
- get_all_cyclo_journeys(self)
- get_all_journeys_for_cyclo(self, cyclo_name)
- get_single_journey_for_cyclo(self, cyclo_name, journey_id)
- get_spin_readings_for_cyclo_journey(self, cyclo_name,
                                      journey_id, page_size, page_state)
- save_spin_reading_for_cyclo_journey(self, cyclo_name, stage_name,
                                      journey_id, data)
```