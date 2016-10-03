# CARTO Map Projections v1

Explore all supported map projections in CARTO.

1. Create a clean dataset of map projections from PostGIS `spatial_ref_sys` table:

  * First, apply the following query in any dataset:

	```sql
	WITH a AS(
	  SELECT 
	    auth_srid,
	    string_to_array(srtext, '"') AS sr_text
	  FROM 
	    spatial_ref_sys
	  )
	SELECT 
	  auth_srid, 
	  sr_text[2] AS geogcs,
	  sr_text[4] AS datum,
	  sr_text[6] AS spheroid,
	  sr_text[16] AS primem,
	  sr_text[22] AS unit
	FROM a
	``
 * Secondly, create a new dataset from this query. Rename it as `map_proj`.

2. Create a map with the Editor with `ne_50m_land` dataset as the unique layer and a color background as basemap.

3. Build a CartoDB.js application with a dropdown menu in order to select a map projection*.

*Notice that only world projections will work.
