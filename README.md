# Data Platform: AVRO Schemas

## General description

This repository contains AVRO schemas of the events in JSON format that can be processed by Data Platform. Currently, all events should follow the same generic format, described by "event_generic" schema, but when necessary add more fields to "attributes" sub-object of "subject" and/or "action" objects of the event.

## Default schema attributes

### Main objects

- **"event_id"** - UUID value, unique identifier of each event.
- **"event_timestamp"** - UTC timestamp of the event as ISO string.
- **"origin"** - describes the type of entity that sent the event (application, browser, backend etc.) and must contain its identifier (device id, browser cookie, backend version, etc.). Usually is equal to the "session_id" of the first session from this origin.
- **"actor"** - specifies the type of entity that initiated the action (customer, user, visitor, etc.) and its identifier (customer id, user email etc.).
- **"subject"** - defines the main subject of the event, towards which the action is aimed, e.g. page, screen, button, order, customer, etc. It also must contain the identifier of the entity (URL, name, internal id, HTML snippet, etc.).
- **"action"** - describes a type of the action taken, in its infinitive form, e.g. view, scroll, click, create (and not clicked or created).

### Possible action attributes

- **"session_id"** - UUID value, identifies the group of events from the same origin, separated in time by no more than 30 minutes in case of a website session, or happening during one run of the application, for example. Usually is equal to the "event_id" of the first event in the session.
- **"timezone_offset"** - Number of hours difference between the local time and UTC.

### Proxy attributes (added during processing)

- **"\_proxy_name", "\_proxy_version"** - name and version of the tool used to ingest, validate and process the events, in our case Apache NiFi.
- **"\_proxy_timestamp"** - UTC timestamp of event ingestion, stored as ISO string.
- **"\_proxy_origin"** - identifier of the event sender from proxy's perspective, usually the IP address.
