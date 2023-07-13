# Table: solace_event_version

In Event Portal, when you update an Event, you can update an existing version or create a new version of the Event. Versions allow you to work on updates and test new versions in development and staging environments while the stable version remains in the production environment. Each version also has a lifecycle state. 

### Key columns
- Provide a numeric `id` if you want to query for a specific Event version. This can be either set directly in a `where` clause, or specified as part of `join` with another table.

### Caveat
- Be careful when requesting all columns (`*`) without using an `id` in the query. To load this data, Steampipe will have to issue multiple API request to retrieve all resources (essentially issuing a paginated queries).

## Examples

### List of all Event Versions

```sql
select
  ev.version as version,
  ev."displayName" as versionName,
  e.name as name
from
  solace_event_version ev
  join
    solace_event e
    on ev."enumId" = e.id
where ev.id = 'n5o41x2fh62';

-- or a simplified version

select
  id, version, displayName
from
  solace_event_version;
```

### Detail of an Event Version

```sql
select
  *
from
  solace_event_version
where
  id = 'n5o4xx2fh62';
```