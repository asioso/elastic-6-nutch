# NUTCH Elastic 6 Indexer Plugin

this just updates the existing elastic indexer to work with ES 6.7
updated dependencies and fixes some namespace and class changes.

# Install/Build
put this source folder (indexer-elastic-6) into nutch's src/plugin directory


## build with nutch

add this line to nutch's build.xml for all targets!
```xml
<ant dir="indexer-elastic-6" target="deploy"/>
```

build this plugin with nutch 

```bash
ant
```

# Configuration

## Index writer configuration:

add your writer configuration in /conf/index-writers.xml

```xml
<writer id="indexer_elastic_6_1" class="org.apache.nutch.indexwriter.elastic6.ElasticIndexWriter">
    <parameters>
      <param name="host" value="0.0.0.0"/>
      <param name="port" value="9300"/>
      <param name="index" value="nutchindex"/>
      <param name="max.bulk.docs" value="250"/>
      <param name="max.bulk.size" value="2500500"/>
      <param name="exponential.backoff.millis" value="100"/>
      <param name="exponential.backoff.retries" value="10"/>
      <param name="bulk.close.timeout" value="600"/>
    </parameters>
    <mapping>
      <copy>
        <field source="title" dest="title,search"/>
      </copy>
      <rename />
      <remove />
    </mapping>
  </writer>

```



## Use this plugin:

enable it in nutch-site.xml

```
<property>
    <name>plugin.includes</name>        
    <value>protocol-httpclient|urlfilter-regex|parse-(html|text|metatags|tika)|index-(basic|anchor|urlmeta|more|metadata)|query-(basic|site|url)|indexer-elastic-6|nutch-extensionpoints|summary-basic|scoring-opic|urlnormalizer-(pass|regex|basic)||language-identifier</value>
</property>
``` 


