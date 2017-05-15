# logback 中配置 perf4j
Perf4j最主要的一个好处就是可以跟log4j或者logback来性能分析和监控线上运行的程序。集成的方式主要是：自定义log4j的appenders通过标准的配置加入到log4j中去（后面会有配置的例子）。有一个要注意的地方就是需要使用log4j的1.2.14版本或者更高版本。perf4j 的 0.9.16 版本开始才能与logback集成.  
由于我一般都是使用logback，所以对于log4j的集成我就不描述了，我觉得应该差不多的。  

Perf4j最重要的appender就是AsyncCoalescingStatisticsAppender，它会把一段时间内StopWatch的信息汇总到一个独立的GroupedTimingStatistics日志信息，然后把这个独立的信息传给下游的appenders，比如fileappenders，这样就可以写到文件中去了。也可以传给per4j的其他自定义appenders.  

接下来我们看一个logback.xml的例子

	<!-- Perf4J appenders -->

    <!-- This file appender is used to output aggregated performance statistics -->
    <appender name="perf4jFileAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <File>${LOG_DIR}/lifeix-dbcontent-api-perf4j.log</File>
        <encoder>
            <Pattern>%date %-5level [%thread] %logger{36} [%file:%line] %msg%n</Pattern>
        </encoder>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <FileNamePattern>${LOG_DIR}/lifeix-dbcontent-api-perf4j.%d{yyyy-MM-dd}.log</FileNamePattern>
        </rollingPolicy>
    </appender>

    <!-- Loggers -->
    <!--
      The Perf4J logger. Note that org.perf4j.TimingLogger is the value of the
      org.perf4j.StopWatch.DEFAULT_LOGGER_NAME constant. Also, note that
      additivity is set to false, which is usually what is desired - this means
      that timing statements will only be sent to this logger and NOT to
      upstream loggers.
    -->
    <logger name="org.perf4j.TimingLogger" additivity="false">
        <level value="INFO"/>
        <appender-ref ref="perf4jFileAppender"/>
    </logger>

配置文件来自于[官方文档][2], 内有更详细的各种appender配置
关于log4j的配置, 在[perf4j使用三（log4j集成）][1]


[1]: http://www.blogjava.net/yangpingyu/archive/2012/04/16/374725.html
[2]: http://perf4j.codehaus.org/apidocs/org/perf4j/logback/package-summary.html