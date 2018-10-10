# Data Platform: AVRO Schemas

## General description

This repository contains AVRO schemas of the events in JSON format that can be processed by Data Platform. All events should follow the same default format, described by EVENT_DEFAULT schema, and when necessary add more attributes in the "content" object of the event. Schema naming convention is EVENT_<CONTEXT>_<OBJECT>_<ACTION>, where "context", "object" and "action" are the mandatory top-level attributes of the event.

## Default schema attributes

### Main attributes

- **"context"** - gives a context to an event - usually where it has occurred. It could be for example WEBSITE, FUNNEL, APPLICATION or maybe ANDROID to be more specific.
- **"object"** - defines on entity, towards which an action was taken, e.g. PAGE, SCREEN, BUTTON, ORDER, CUSTOMER, etc. Can be accompanied by "object_id" attribute, providing the identifier of the entity (URL, name, internal id, HTML snippet, etc.).
- **"action"** - describes an action taken, in its infinitive form, e.g. VIEW, SCROLL, CLICK, CREATE (and not CLICKED or CREATED).
- **"origin"** - describes what sent the event (APPLICATION, BROWSER, BACKEND etc.) and can be accompanied by "object_id" attribute as its identifier (device id, browser cookie, backed version, etc.). Usually is equal to the "session_id" of the first session from this origin.
- **"actor"** - whenever possible, "action" should be accompanied by an "actor" attribute, specifying who initiated the action (CUSTOMER, USER, etc.), and "actor_id" as the identifier (customer id, user email etc.).
- **"session_id"** - UUID value, identifies the group of events from the same origin, separated in time by no more than 30 minutes in case of a website session, or happening during one run of the application, for example. Usually is equal to the "event_id" of the first event in the session.
- **"event_id"** - UUID value, unique identifier of each event.
- **"event_timestamp"** - UTC timestamp of the event as ISO string.
- **"timezone_offset"** - Number of hours difference between the local time and UTC.
- **"schema_version"** - version of the schema, used to encode the current event.

### Proxy attributes (added during processing)

- **"\_proxy_name", "\_proxy_version"** - name and version of the tool used to ingest, validate and process the events, in our case Apache NiFi.
- **"\_proxy_timestamp"** - UTC timestamp of event ingestion, stored as ISO string.
- **"\_proxy_origin"** - identifier of the event sender from proxy's perspective, usually the IP address.

## Examples

Format:
*context/object-<object_id>/action/origin-<origin_id>/actor-<actor_id>*

- WEBSITE/PAGE-<url>/VIEW/BROWSER-<uuid>
- WEBSITE/LINK-<html>/CLICK/BROWSER-<uuid>
- WEBSITE/BUTTON-<html>/CLICK/BROWSER-<uuid>
- ANDROID/SCREEN/TURN_ON/DEVICE-<uuid>
- ANDROID/SCREEN/TURN_OFF/DEVICE-<uuid>
