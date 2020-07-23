---
title: Data Access
weight: 30
---
# Data Access

## sessionManager(object)
- get_instance()
- save_credentials(self, username, password, keyspace, secure_connection_bundle_path)
- test_credentials(self, username, password, keyspace, secure_connection_bundle_path)
- connect(self)
- check_connection(self)
- close(self)

## cycloJourneyCatalogDAO(object)

- maybe_create_schema(self)
- write_journey(self, cyclo_name, journey_id, start, end, active, summary)
- get_all_journeys(self)
- get_all_journeys_for_cyclo(self, cyclo_name)
- get_single_journey_for_cyclo(self, cyclo_name, journey_id)

## cycloSpinDAO(object)

- maybe_create_schema(self)
- write_readings(self, cyclo_name, stage_name, journey_id, data)
- get_spin_readings_for_journey(self, cyclo_name, journey_id, page_size=25, page_state=None)
