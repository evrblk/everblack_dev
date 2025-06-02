---
title: Concepts
type: docs
layout: bison
aliases:
  - /docs/bison/
---


# Main concepts

## Time Series

__Time Series__ is a series of data points with corresponding timestamps.



## Storage and organization




## Data Types

Bison is a strongly typed system. It supports several primitive data types as well as complex types.

* `INTEGER` - 64-bit signed integer numbers
* `FLOAT` - Double-precision floating point numbers
* `STRING` - Unicode strings of text up to 256Kb long
* `BOOLEAN` - `True` or `False`
* `STRUCT[MY_STRUCT_NAME]` - Structures with fields of all types. Nested structures are supported. Recursive structures (structures which include themselves) are not supported. 
* `ENUM[MY_ENUM_NAME]` - A type with a limited number of possible values. Represented as strings.

Data type is assigned to a time series at creation and cannot be changed later. All ingested data is validated, and it is guaranteed that no time series can contain a mix of data of several data types in different moments of time. 

Users can define their own structures and enums. Bison also provides some commonly used structures.

## Archives

__Archive__ is a logical grouping of time series with common settings. Archives are not a physical grouping, time series data is not collocated together, and archives are not presenting any limits on time series in them.

All time series in an archive share common settings:

* Hot Tier configuration 
  * Retention period - for how many days in the past values are stored
* Cold Tier configuration
* Authorization

Storage space is one of the pricing dimensions in Bison (see more [here]()). Users are charged for all the space occupied by all time series within archives. The main rationale behind splitting time series in different archives is the cost optimization. It makes sense to store higher frequency data (for example, 1s) for shorter periods of time (weeks) and store aggregated/down-sampled data (1m or less) for longer (years).

Time series are identified only by their IDs, there are no names or other metadata. There is no search of time series within an archive of any kind. There is no `ListTimeSeries` API, because it does not make much sense to scroll through a list of thousands of time series without any human-readable name or metadata. Items and Directories are the prime mean of organization and indexing.

A time series cannot be moved from one archive to another. However, it is possible to clone a time series by fully reading it from a source archive and writing the same data to a destination time series in another archive.

## Items and Directories

__Directories__ are simply a way to organize large numbers of items into a tree structure and navigate it. This is very similar to file systems. Names of subdirectories must be unique within a directory. But names dot need to be globally unique.

__Items__ are

There are few service limits:

* Maximum depth of a tree: 20
* Maximum number of children (subdirectories and items) in a directory: 1024

All directories and items have their own immutable IDs which are independent of a particular place/path of those directories or items in the tree. It means that existing readers and writers of time series data will not be affected by moving a directory or an item into another directory. This allows to reorganize the structure over time as it grows or when a need for improvement arises without affecting existing formulas, aggregates, dashboards, or other readers, as well as all existing writers/importers. 

Safety and invariants enforcement are the most important property of this items+directories organization.

* A directory cannot be deleted if it has items or subdirectories.
* A directory cannot be moved into its own child and create a cycle in a tree.
* An item cannot be removed if it is referenced by any other item (formula, aggregate, alarm, etc).
* A directory cannot be moved into another directory if there is already 

## Buckets


