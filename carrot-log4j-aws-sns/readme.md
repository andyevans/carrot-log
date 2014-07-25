<!--

    Copyright (C) 2010-2013 Andrei Pozolotin <Andrei.Pozolotin@gmail.com>

    All rights reserved. Licensed under the OSI BSD License.

    http://www.opensource.org/licenses/bsd-license.php

-->
### inspired by actual events

all of these great projects lacked some features that we needed:

[Adrian Petrescu / amazon-sns-log4j-appender]
(https://github.com/apetresc/amazon-sns-log4j-appender)

[Edson Yanaga / log4j-sns]
(https://github.com/insula/log4j-sns)

[Paul Smith / json-log4j-layout]
(https://github.com/Aconex/json-log4j-layout)


### features of current project

so we made a new one:

* comes as an osgi bundle

* has configurable thread pool

* uses json event layout by default

* has configurable json event renderer 

* has configurable topic and subject

* uses event throttle based on write time eviction

* uses decoupled dependencies (maven scope provided)

* reads amazon credentials from external file

* does not try to create topics on demand (security requirement)

* uses configurable event signature mask for event cache/throttle  

### release repo
[maven central](http://search.maven.org/#search%7Cga%7C1%7Ccarrotgarden)

### snapshot repo
[sonatype snapshots](https://oss.sonatype.org/content/repositories/snapshots/)

### example log4j.properties - no credentials file, passing aws region and log4j pattern output
```
log4j.appender.SNS=com.carrotgarden.log4j.aws.sns.Appender
log4j.appender.SNS.threshold=INFO
#log4j.appender.SNS.credentials=${user.home}/.amazon/publish-notification.properties
log4j.appender.SNS.region=AP_SOUTHEAST_2
log4j.appender.SNS.accessKey=YOUR_ACCESS_KEY
log4j.appender.SNS.secretKey=YOUR_SECRET_KEY
log4j.appender.SNS.topicName=carrot-tester
log4j.appender.SNS.topicSubject=karaf.company.com
log4j.appender.SNS.evaluatorClassName=com.carrotgarden.log4j.aws.sns.EvaluatorThrottler
log4j.appender.SNS.evaluatorProperties= period=10 \n unit=SECONDS \n mask=LOGGER_NAME,LINE_NUMBER
log4j.appender.SNS.layout=org.apache.log4j.PatternLayout
log4j.appender.SNS.layout.ConversionPattern=%d [%t] %-5p %c - %m%n

### example log4j.properties - using credentials file and json output
```
log4j.appender.SNS=com.carrotgarden.log4j.aws.sns.Appender
log4j.appender.SNS.threshold=INFO
log4j.appender.SNS.credentials=${user.home}/.amazon/publish-notification.properties
log4j.appender.SNS.topicName=carrot-tester
log4j.appender.SNS.topicSubject=karaf.company.com
log4j.appender.SNS.evaluatorClassName=com.carrotgarden.log4j.aws.sns.EvaluatorThrottler
log4j.appender.SNS.evaluatorProperties= period=10 \n unit=SECONDS \n mask=LOGGER_NAME,LINE_NUMBER
log4j.appender.SNS.layout=com.carrotgarden.log4j.aws.sns.LayoutJSON
log4j.appender.SNS.layout.UsePrettyPrinter=true
```
