---
syntax:
---

Return information and statistics on the index

## Syntax

{{< highlight bash >}}
FT.INFO index
{{< / highlight >}}

[Examples](#examples)

## Required parameters

<details open>
<summary><code>index</code></summary>

is full-text index name. You must first create the index using `FT.CREATE`.
</details>

## Return

FT.INFO returns an array reply with pairs of keys and values.

Returned values include:

- `index_definition`: reflection of `FT.CREATE` command parameters.
- `fields`: index schema - field names, types, and attributes.
- Number of documents.
- Number of distinct terms.
- Average bytes per record.
- Size and capacity of the index buffers.
- Indexing state and percentage as well as failures:
  - `indexing`: whether of not the index is being scanned in the background.
  - `percent_indexed`: progress of background indexing (1 if complete).
  - `hash_indexing_failures`: number of failures due to operations not compatible with index schema.

Optional statistics include:

* `garbage collector` for all options other than NOGC.
* `cursors` if a cursor exists for the index.
* `stopword lists` if a custom stopword list is used.

## Examples

<details open>
<summary><b>Return statistics about an index</b></summary>

{{< highlight bash >}}
redis> FT.CREATE idx SCHEMA fieldName TEXT
OK
redis> FT.INFO idx
 1) index_name
 2) idx
 3) index_options
 4) (empty array)
 5) index_definition
 6) 1) key_type
    2) HASH
    3) prefixes
    4) 1) 
    5) default_score
    6) "1"
 7) attributes
 8) 1) 1) identifier
       2) fieldName
       3) attribute
       4) fieldName
       5) type
       6) TEXT
       7) WEIGHT
       8) "1"
 9) num_docs
10) "0"
11) max_doc_id
12) "0"
13) num_terms
14) "0"
15) num_records
16) "0"
17) inverted_sz_mb
18) "0"
19) vector_index_sz_mb
20) "0"
21) total_inverted_index_blocks
22) "0"
23) offset_vectors_sz_mb
24) "0"
25) doc_table_size_mb
26) "0"
27) sortable_values_size_mb
28) "0"
29) key_table_size_mb
30) "0"
31) records_per_doc_avg
32) "-nan"
33) bytes_per_record_avg
34) "-nan"
35) offsets_per_term_avg
36) "-nan"
37) offset_bits_per_record_avg
38) "-nan"
39) hash_indexing_failures
40) "0"
41) total_indexing_time
42) "0"
43) indexing
44) "0"
45) percent_indexed
46) "1"
47) gc_stats
48)  1) bytes_collected
     2) "0"
     3) total_ms_run
     4) "0"
     5) total_cycles
     6) "0"
     7) average_cycle_time_ms
     8) "-nan"
     9) last_run_time_ms
    10) "0"
    11) gc_numeric_trees_missed
    12) "0"
    13) gc_blocks_denied
    14) "0"
49) cursor_stats
50) 1) global_idle
    2) (integer) 0
    3) global_total
    4) (integer) 0
    5) index_capacity
    6) (integer) 128
    7) index_total
    8) (integer) 0
{{< / highlight >}}
</details>

## See also

`FT.CREATE` | `FT.SEARCH`

## Related topics

[RediSearch](/docs/stack/search)

