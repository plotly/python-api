---
jupyter:
  jupytext:
    notebook_metadata_filter: all
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.4
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.11.10
  plotly:
    description: Guide to changes in version 6 of Plotly.py and how to migrate from
      version 5
    display_as: file_settings
    language: python
    layout: base
    name: Changes in Version 6
    order: 8
    page_type: example_index
    permalink: python/v6-migration/
    thumbnail: thumbnail/v4-migration.png
---

This page outlines the changes in Plotly.py version 6 and cases where you may need to update your charts or tools that you use for working with Plotly.py.

<!-- #region -->
## Jupyter Notebook Support

Versions of Jupyter Notebook earlier than version 7 are no longer supported. To upgrade to the latest Jupyter Notebook:

```
pip install notebook --upgrade
```

## Change to anywidget for go.FigureWidget

[go.FigureWidget](https://plotly.com/python/figurewidget/) now uses [anywidget](https://anywidget.dev/). Install `anywidget` with:


```python
pip install anywidget
```

## Processing NumPy and NumPy-Convertible Arrays

Plotly.py now takes advantage of recent changes in how Plotly.js handles typed arrays for improved performance. See the [performance page](python/performance/) for more details.

## Removed Attributes

The following attributes have been removed in Plotly.py 6.

### `titlefont`,`titleposition`, `titleside`, and `titleoffset`

The `titlefont`,`titleposition`, `titleside`, and `titleoffset` attributes have been removed. Replace them with `title.font`, `title.position`, `title.side`, and `title.offset`.

Here's an example using `layout.titlefont`:

```python
import plotly.graph_objects as go

trace = go.Bar(
    x=['A', 'B', 'C', 'D'],
    y=[10, 15, 13, 17]
)

layout = go.Layout(
    title=dict(
        text='Chart Title'
    ),
    titlefont=dict(
        size=40
    )
)

fig = go.Figure(data=[trace], layout=layout)

fig.show()
```

Updated to use `layout.title.font`:


```python
import plotly.graph_objects as go

trace = go.Bar(
    x=['A', 'B', 'C', 'D'],
    y=[10, 15, 13, 17]
)

layout = go.Layout(
    title=dict(
        text='Chart Title',
        font=dict(size=40)
    )
)

fig = go.Figure(data=[trace], layout=layout)

fig.show()
```

## Removed Traces

The following traces have been removed.

### `heatmapgl`

The `heatmapgl` trace has been removed. Use [`heatmap`](/python/heatmaps/) instead.


### `pointcloud`

The `pointcloud` trace has been removed. Use [`scattergl`](/python/reference/scattergl/).

<!-- #endregion -->

## Other Removed Features

### Transforms

Transforms, which were deprecated in Plotly.py v5, have been removed. You can achieve similar functionality by preprocessing the data with a DataFrame library.

For example, a transform to filter the data:

```python
  dict(
    type = 'filter',
    target = df['year'],
    orientation = '=',
    value = 2007
  ),
```

Could be rewritten using Pandas:

```python
df_2007 = df[df['year'] == 2007]
```