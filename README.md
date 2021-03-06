<html>
<head>
<meta charset="UTF-8">
<title>logstash for SCAPI - filter scapivot</title>
<link rel="stylesheet" href="http://logstash.net/style.css">
</head>
<body>
<div class="container">

<div id="content_right">
<!--main content goes here, yo!-->
<div class="content_wrapper">

<h2>scapivot</h2>
<h3>Milestone: <a href="http://logstash.net/docs/1.4.2/plugin-milestones">1</a></h3>
<h3> Synopsis </h3>
Receives a stream of events and pivots them from 'skinny' to 'wide' (also known as a 'Vertical' pivot in DataStage)
It groups the events into sets with the same <code>window_column</code> (see below) and pivots each set.
<p>
<pre><code>filter {
  scacsv {
    <a href="#window_column">window_column</a> => ... # string (required)
    <a href="#fixed_columns">fixed_columns</a> => ... # array (required)
    <a href="#target_column">target_column</a> => ... # string (required)
    <a href="#value_column">value_column</a> => ... # string (required)
    <a href="#flush_interval">flush_interval</a> => ... # number (optional), default: 60
   }
}
</code></pre>
<h3> Details </h3>
<p>
As events come in, those that have matching values for <code>window_column</code> are buffered. Once a new event with a different value for <code>window_column</code> arrives, the buffered events will be pivoted and a new set of events output. Pivoting is achieved by selecting all the unique <code>fixed_columns</code> sets, and for each of those sets, determining the values from the corresponding <code>target_column</code>s. Those values are output in new events with a set of columns for the <code>fixed_columns</code> and columns for each unique <code>value_column</code>
</p>
<h4>
<a name="window_column">
window_column
</a>
</h4>
<ul>
<li> Value type is <a href="http://logstash.net/docs/1.4.2/configuration#string">String</a> </li>
<li> There is no default for this setting </li>
</ul>
<p>Field used to group data within a window, prior to pivoting. For SCAPI, this is generally the timestamp field</p>
<h4>
<a name="fixed_columns">
fixed_columns
</a>
</h4>
<ul>
<li> Value type is <a href="http://logstash.net/docs/1.4.2/configuration#string">String</a> </li>
<li> There is no default for this setting </li>
</ul>
<p>
Set of field names which will be used to uniquely identify a set of rows. All rows with the same values for fixed_columns will have their pivoted values assigend to a single output row (event)
</p>
<h4>
<a name="target_column">
target_column
</a>
</h4>
<ul>
<li> Value type is <a href="http://logstash.net/docs/1.4.2/configuration#string">string</a> </li>
<li> There is no default for this setting </li>
</ul>
<p>
Name of field where the identity of the field in the produced pivoted row is to be found
</p>
<h4>
<a name="value_column">
value_column
</a>
</h4>
<ul>
<li> Value type is <a href="http://logstash.net/docs/1.4.2/configuration#dytomh">string</a> </li>
<li> There is no default value for this setting. </li>
</ul>
<p>
This configuration setting is used to identify the field in the input tuple/column which contains the metric values.
</p>
<h4>
<a name="flush_interval">
flush_interval
</a>
</h4>
<ul>
<li> Value type is <a href="http://logstash.net/docs/1.4.2/configuration#string">string</a> </li>
<li> There is no default for this setting </li>
</ul>
<p>
Amount of time (seconds) to wait before pivoting and flushing the currently cached events. In normal steady-state event flow, an event with a new value for <code>window_column</code> will trigger a pivot and flush, but if the event is the last one in a series, then an alternative mechanism, such as this timer-based one, is needed to trigger the pivot and flush.
</p>
<hr>
</div>
<div class="clear">
</div>
</div>
</div>
<!--closes main container div-->
<div class="clear">
</div>
<div class="footer">
<p>
Hello! I'm your friendly footer. If you're actually reading this, I'm impressed.
</p>
</div>
<noscript>
<div style="display:inline;">
<img height="1" width="1" style="border-style:none;" alt="" src="//googleads.g.doubleclick.net/pagead/viewthroughconversion/985891458/?value=0&amp;guid=ON&amp;script=0"/>
</div>
</noscript>
<script src="/js/patch.js?1.4.2"></script>
</body>
</html>
