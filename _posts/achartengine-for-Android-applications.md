---
title: achartengine for Android applications
date: 2017-11-17 06:37:53
tags:
- Android
- PlugIn
categories: 'Android'
---
Chartengine is an Android data -> chart plugin.
Charting library for Android applications. Automatically exported from code.google.com/p/achartengine.AChartEngine is a charting library for Android applications.

Its major components are used as follow:
{% codeblock lang:java%}
XYMultipleSeriesDataset mDataset = getDataSet();
XYMultipleSeriesRenderer mRenderer = getRenderer();
setRendererStyling(mRenderer);
mChartView = ChartFactory.getLineChartView(mContext,mDataset,mRenderer);
{% endcodeblock %}
### XYMultipleSeriesDataset:
This should be a list that contain one or more DataSourceObject.
For example:(Note: This code is just example, do not dirctly copy and use)
```
public XYMultipleSeriesDataset getDataSet(){
	XYMultipleSeriesDataset dataset = new XYMultipleSeriesDataset();
	DataSource xyDataSource = new DataSource;
	xyDataSource.setXYValues();//xyDataSource[(x1,y1),(x2,y2)];
	dataset.addSeries(xyDataSource);
	return dataset;
}
```

### XYMultipleSeriesRenderer:
This should be a list of render that 1 to 1 mapping with the DataSourceObject.
For example:
```
public XYMultipleSeriesRenderer getRenderer(){
	XYMultipleSeriesRenderer renderer = new XYMultipleSeriesRenderer();
	XYSeriesRenderer r = new XYSeriesRenderer();
	r.setColor; ... etc
	render.addSeriesRenderer(r);
	return render;
}
```
then if we like we can set some render styling for the XYMultipleSeriesRenderer above: setRendererStyling(mRenderer);

### Finially we call lib function:
```
ChartFactory.getLineChartView(context,mDataset,mRenderer);
```

Today I do faced an issue. I have four DataSet and four Renderer setup. However when the graph is render, In the condition of no data for one of the dataSet the other dataset will not show. That is if one of the dataset is like this[(0,0)]. this other dataSet is not showing. I did the check 4 renderer and 4 dataset are all created. I have not find out the solution for that. Will keep this post update.
Reason: So the problem appear that the hour diff data (X-axis) is not plotted without DataA and DataB data(I guess the first dataset have to have number not (0,0)). Hence the starttimeSeries and the endtimeSeries is not recognized the x-axis value;
solution:(Note, here it is not matter what we are using, DataA.add or DataB.add for starttimeSeries and endtimeSeries. we just need to borrow the objcet that should not be null to show on the graph)
```
if (DataA.getItemCount() == 0){
	if (StartTimeSeries.getItemCount() > 0){
        	double d1 = StartTimeSeries.getX(0);
                double d2 = StartTimeSeries.getY(0);
                DataA.add(d1, d2);

                double d3 = EndTimeSeries.getX(0);
                double d4 = EndTimeSeries.getY(0);
                DataB.add(d3, d4);
        }
}
```
