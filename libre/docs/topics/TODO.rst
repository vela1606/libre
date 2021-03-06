PENDING
-------
* Filebased sources

  * Add compressed file support
  * Skip blank lines?
  * Switch from column widths to column ranges
  * Toggable auto update via inotify, polling or python-watchdog
  * Add internal support for open ranges for rows "10-"
  * Migrate Spreadsheet regex import and skip solution to other filebased sources
  * Add row number exclusion support during import

* Database sources

  * Add DB Source support

    * Pony ORM


* Documentation

  * Release notes
  * Getting started
  * Add better sample source files

    * http://www.census.gov/population/estimates/puerto-rico/prmunnet.txt

  * Examples using existing public data


* General

  * Parse values

    * True values, False values

  * Add Relationship support
  * Specify number of versions to keep, deleting old ones
  * Add instructions to sources, per source type
  * Add row number exclusion support during import
  * Stored JSON data index support
  * JSON source descriptor export and import
  * Rename timestamp to version and allow user defined version strings
  * Data translation
  * Remap JSON names


* Geographical sources

  * <No task remains>


* Job processing

  * Add Celery support or subprocess


* LQL

  * LQL based pagination (size and page number) (Andres Colón)
  * Expand the _fields directive to support dot and index notations
  * Sorting

    * _order=<field name>,<field name>
    * sort(+field_name,-field_name)
    * Ascending (field name)
    * Descending (-field name)

  * Add range exclusion

    * _xrange, _not_in_range, _nrange

  * Add regex support

    * _match

  * Subqueries
  * Aggregation

    * Grouping
    * Sum

  * Pagination
  * Limiting

    * _limit=<soft limit of elements>

  * Skipping results

    * _skip=<number of elements>
    * _first
    * _last
    * _one

      * Return error if more than one

  * Combined

    * _limit=(count, start, maxCount)

  * Joins between datasets

    * _join=<data set name>,<join type>,<current set field>__<foreign set field>,<current set field>__<foreign set field>
    * _relation=(field, subquery)

  * Add support for annotations
  * Field selection

    * _select=(field_name, field_name)

  * _distinct
  * Not in = out
  * _excludes

* Output

  * Add support for generating output formats other than JSON

    * Shapefiles
    * GeoJSON - DONE
    * CSV
    * Excel
    * XML - DONE
    * NIEM
    * Fixed width

* Web services sources

  * Add caching support to WS Sources

    * TTL support

* Unsorted

  * Improve output logging - INPROGRES
  * Empty but valid queries should return HTTP404 or HTTP200 with '{"status": "Not found"}'
  * Show required argument for WS
  * Interpret WS arguments
  * Result count
  * Fix upload_to
  * Calculate geometries area, size, lenghts in pin template
  * Delete stored source files when a source is deleted
  * Delete stored source files when a new file is uploaded
  * Fix JsonField not returning dates or times only datetimes
  * Move _fields parsing to allow being parsed on get_one method
  * Optimize AND type join
  * Use islice
  * Dataset human browser
  * Data store browser
  * Add support for item-based and result-based evaluation
  * Add support for JSON Pointer
  * Add support for displaying map titles
  * Add support for dynamic icons for the map renderer

    * http://tools.ietf.org/html/draft-ietf-appsawg-json-pointer-09

  * Add support for RQL

    * http://www.sitepen.com/blog/2010/11/02/resource-query-language-a-query-language-for-the-web-nosql/
    * http://rql-engine.eu01.aws.af.cm/


  * Add support for JSON Query

    * http://dojotoolkit.org/reference-guide/1.9/dojox/json/query.html
    * http://www.sitepen.com/blog/2008/07/16/jsonquery-data-querying-beyond-jsonpath/

  * Add support for JSONgrep

    * http://blogs.fluidinfo.com/terry/2010/11/25/jsongrep-py-python-for-extracting-pieces-of-json-objects/

  * Migrate DatabaseSource's get_one and get_all solution to other source classes
  * Get rid of WSResultField WSArgument and use SourceColumnBase instead
  * Icon preview in admin
  * Add webhooks support

    * https://github.com/johnboxall/django_webhooks

  * Regex support for Fixed width sources
  * Add view type source
  * Improve _flatten predicate
  * Add dumb result caching

   * Hash query + hash of sources = key: value = result

  * Add custom response header values

    * X-LIBRE-count
    * X-LIBRE-query

    * response = Response(result)
      response['X-LIBRE-count'] = count
      return response

  * Get rid of fetch_all on the DB backend

    * cursor.rowcount

    def dictfetchall(cursor):
        "Returns all rows from a cursor as a dict"
        desc = cursor.description
        return [
            dict(zip([col[0] for col in desc], row))
            for row in cursor.fetchall()
        ]

    from itertools import *
    from django.db import connection

    def query_to_dicts(query_string, *query_args):
    """Run a simple query and produce a generator
        that returns the results as a bunch of dictionaries
        with keys for the column values selected.
        """
    cursor = connection.cursor()
    cursor.execute(query_string, query_args)
    col_names = [desc[0] for desc in cursor.description]
    while True:
        row = cursor.fetchone()
        if row is None:
            break
        row_dict = dict(izip(col_names, row))
        yield row_dict
    return

  * Improve sort with Sort generators

    * https://gist.github.com/rbonvall/18896
    * http://www.ics.uci.edu/~eppstein/161/python/mergesort-generators.py

  * Dynamic icons
