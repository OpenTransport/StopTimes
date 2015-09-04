# The Specification

## Prefixes used

| namespace prefix | URI |
|----:|:----|
| st: |`http://semweb.mmlab.be/ns/stoptimes#` |
| gtfs: |`http://vocab.gtfs.org/terms#` |
| dct:| `http://purl.org/dc/terms/` |
| xsd:| `http://www.w3.org/2001/XMLSchema#`|
| rdfs:| `http://www.w3.org/2000/01/rdf-schema#`|
| foaf:| `http://xmlns.com/foaf/0.1/`|

## Schema overview

When we want to identify the action where a vehicle stops at a certain moment on a certain place, and departs again, we can give that thing a type [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime). When we only want to identify the action of arriving at a certain stop, or departing at a certain stop, we also make available the types [st:Arrival](http://semweb.mmlab.be/ns/stoptimes#Arrival) and [st:Departure](http://semweb.mmlab.be/ns/stoptimes#Departure).

A [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime) has to have a [gtfs:arrivalTime](http://vocab.gtfs.org/terms#arrivalTime), [dct:date](http://purl.org/dc/terms/date) and/or a [gtfs:departureTime](http://vocab.gtfs.org/terms#departureTime). If an arrivalTime or a departureTime is not set, it may indicate the vehicle is at a terminus or it is starting its service.

The [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime) also refers through [gtfs:stop](http://vocab.gtfs.org/terms#stop) to a [gtfs:Stop](http://vocab.gtfs.org/terms#Stop), pointing to the exact location where passengers can disembark and embark. Mind that the [gtfs:stop](http://vocab.gtfs.org/terms#stop) can change over time for the same [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime). For example, one [gtfs:Stop](http://vocab.gtfs.org/terms#Stop) can be "platform A of Paris Gare du Nord", but due to the late announcement of the exact platform at Paris Gare du Nord, first the [gtfs:Station](http://vocab.gtfs.org/terms#Station) "Paris Gare du Nord" can be mentioned before the precise [gtfs:Stop](http://vocab.gtfs.org/terms#Stop) is mentioned.

The [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime) may refer, using the predicate [st:nextStopTime](http://semweb.mmlab.be/ns/stoptimes#nextStopTime), to the next [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime). Mind that this can also change over time, e.g., for an extra stop being introduced on the current [gtfs:Trip](http://vocab.gtfs.org/terms#Trip).

An [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime) is very similar to a [gtfs:StopTime](http://vocab.gtfs.org/terms#StopTime). While [gtfs:StopTime](http://vocab.gtfs.org/terms#StopTime) defines a collection of recurring stop times, [st:StopTime](http://semweb.mmlab.be/ns/stoptimes#StopTime) only identifies one specific stop time.

Other GTFS terms that are interesting to be used include, but are not limited to, [gtfs:route](http://vocab.gtfs.org/terms#route) or [gtfs:trip](http://vocab.gtfs.org/terms#trip), [gtfs:headsign](http://vocab.gtfs.org/terms#headsign). More about gtfs can be found at https://github.com/OpenTransport/linked-gtfs/blob/master/spec.md

Another interesting vocabulary to use is the [Linked Connections vocabulary (lc:)](http://github.com/linkedconnections/vocabulary).

# Example usage

## Stoptime list

Use a JSON-LD context and mark up your JSON:
```json
{
  "@context" : {
    "gtfs" : "http://vocab.gtfs.org/terms#",
    "dct" : "http://purl.org/dc/terms/",
    "st": "http://semweb.mmlab.be/ns/stoptimes#",
    "arrivaltime" : "gtfs:arrivalTime",
    "departuretime" : "gtfs:departureTime",
    "date" : "dct:date",
    "headsign" : "gtfs:headsign",
    "stop" : "gtfs:stop",
    "route" : {
      "@id" : "gtfs:route",
      "@type" : "@id"
    },
    "accessibility" : {
      "@id" : "gtfs:wheelchairAccessible",
      "@type" : "@id"
    },
    "name" : "http://xmlns.com/foaf/0.1/name"
  },
  "@graph" : {
    "@id" : "http://example.com/stop_times/1",
    "@type" : "st:StopTime",
    "arrivaltime" : "19:19:00",
    "departuretime" : "19:16:00",
    "date" : "2014-11-03",
    "stop" : {
      "@id" : "http://irail.be/stations/NMBS/008896412",
      "@type" : "gtfs:Station",
      "name" : "Comines",
      "accessibility" : "gtfs:WheelchairAccessible"
    },
    "headsign" : "Poperinge",
    "accessibility" : "gtfs:WheelchairAccessible",
    "route" : "http://example.com/routes/1"
  }
}
```
