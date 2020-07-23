---
title: Model
weight: 20
---
# Model

## CycloJourneyCatalog

```python
class CycloJourneyCatalog(object):

    def __init__(self, cyclo_name, journey_id, start, end, active, summary):
        self.cyclo_name = cyclo_name
        self.journey_id = uuid_from_string(journey_id)
        self.start = format_timestamp(start)
        self.end = format_timestamp(end)
        self.active = active
        self.summary = summary
```

## CycloSpin

```python
class CycloSpin(object):

    def __init__(self, cyclo_name, journey_id, data):
        self.cyclo_name = cyclo_name
        self.journey_id = uuid_from_string(journey_id)
        self.spin = float(data.get('spin'))
        self.spin_unit = data.get('spin_unit', '#/t')
        self.reading_time = format_timestamp(data.get('reading_time'))
```

## Stage

```python
class Stage(object):

    def __init__(self, stage_name, cyclo_name, timestep):
        self.stage_name = stage_name
        self.cyclo_name = cyclo_name
        self.timestep = timestep
        self.spin = float(data.get('spin'))
        self.spin_unit = data.get('spin_unit', '#/t')
        self.reading_time = format_timestamp(data.get('reading_time'))
```

## Product

```python
class Product(object):

    def __init__(self, product_name):
        self.product_name = product_name
```
