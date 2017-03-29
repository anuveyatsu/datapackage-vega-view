# How to specify datapackage view in Vega spec

## Data Package Views Specification

Data Package Views ("Views") define data views such as graphs or tables based on the data in a Data Package.

Views are defined in the `views` property of the Data Package descriptor.

`views` MUST be an array. Each entry in the array MUST be an object. This object MUST follow the Data Package View specification set out here.

A View MUST have the following form:

```javascript=
{
  // generic metadata
  "name": "..."   // unique identifier for view within list of views. (should we call it id ?)
  "title": "My view" // title for this graph

  // data sources for this spec
  "resources": [ resource1, resource2 ]  

  "specType": "" // one of simple | plotly | vega
  // graph spec
  "spec":
}
```


### Vega Spec - an instruction of how to use Vega spec in a datapackage views

*We are using vega as an input: raw vega plus a few tweaks to support data input out of line from their spec (e.g. resources)*

This is straight-up Vega. The only modification that we leave out data references (where we need to know a table name we can rely on the names in the resources array).

In this repo we use example from http://vega.github.io/vega-editor/?mode=vega&spec=barley/

```javascript=
{
  "width": 200,
  "height": 720,

  // NOTE: data property is MISSING here!

  "scales": [
    {
      "name": "g",
      "type": "ordinal",
      "range": "height",
      "padding": 0.15,
      "domain": {
        "data": "barley", "field": "site",
        "sort": {"field": "yield", "op": "median"}
      },
      "reverse": true
    },
    ...
  ...
}
```

To understand how this fits together with the overall spec here's the full view -- note there is nothing about the data because we have a single resource and it gets referenced by default. Alternatively, we can explicitly define which resource to use by passing its index or name in the `resources` property.

```javascript=
{
  "title": "DEMO Vega dp view",
  "specType": "vega",
  "spec": {
    "width": 200,
    "height": 720,
    "scales": [
      {
        "name": "g",
        "type": "ordinal",
        "range": "height",
        "padding": 0.15,
        "domain": {
          "data": "barley", "field": "site",
          "sort": {"field": "yield", "op": "median"}
        },
        "reverse": true
      },
      ...
    ...
  }
}
```

**Note** that `specType` is set to `vega`.
