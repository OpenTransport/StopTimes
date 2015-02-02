# Stop Times vocabulary

### Editors

 * Pieter Colpaert (Open Knowledge | iMinds - Ghent University - MultiMedia Lab)
 * Andrew Byrd (Conveyal)

## Context

The stop times vocabulary is created as a set of URIs to describe the act where a certain vehicle arrives at a certain stop at a certain moment in time and also leaves towards a next stop and plans to arrive at a certain moment in time.

You can use this vocabulary to:
 * annotate your route planning result documents with URIs for a certain stop time, and its predicates and objects,
 * give an overview of the next stop times (arrivals/departures) in a certain stop_area

Check out the json-ld folder for contexts that you can use for your own API

Mind that Stop Times is a very uncompressed specification and doesn't contain ways to describe recurring events (you should use GTFS for that).
