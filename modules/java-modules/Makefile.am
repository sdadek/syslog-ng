if ENABLE_JAVA_MODULES

export GRADLE_OPTS

JAVA_MOD_DST_DIR=$(DESTDIR)/$(moduledir)/java-modules
MOD_JARS=$(shell find $(abs_top_builddir)/modules/java-modules -name '*.jar' -not -path "$(abs_top_builddir)/modules/java-modules/.gradle/*")
JAVA_MODULES_INSTALLED_JARS=$(shell find $(JAVA_MOD_DST_DIR) -name '*.jar')
GRADLE_WORKDIR=$(abs_top_builddir)/modules/java-modules/.gradle

java-modules: $(SYSLOG_NG_CORE_JAR)
	$(AM_V_GEN) $(GRADLE) --project-cache-dir $(GRADLE_WORKDIR) -g $(GRADLE_WORKDIR) -p $(abs_top_srcdir)/modules/java-modules -PsyslogBuildDir=$(abs_top_builddir)/modules/java-modules -PsyslogDepsDir=$(abs_top_builddir)/modules/java/syslog-ng-core/libs build

all-local: java-modules

log4j-copy-jar:
	$(AM_V_GEN) $(GRADLE) --project-cache-dir $(GRADLE_WORKDIR) -g $(GRADLE_WORKDIR) -p $(abs_top_srcdir)/modules/java-modules -PsyslogBuildDir=$(abs_top_builddir)/modules/java-modules -PsyslogDepsDir=$(abs_top_builddir)/modules/java/syslog-ng-core/libs -PjarDestDir=$(JAVA_MOD_DST_DIR) copyLog4j

jest-copy-jar:
	$(AM_V_GEN) $(GRADLE) --project-cache-dir $(GRADLE_WORKDIR) -g $(GRADLE_WORKDIR) -p $(abs_top_srcdir)/modules/java-modules -PsyslogBuildDir=$(abs_top_builddir)/modules/java-modules -PsyslogDepsDir=$(abs_top_builddir)/modules/java/syslog-ng-core/libs -PjarDestDir=$(JAVA_MOD_DST_DIR) copyJestRuntimeDeps

java-modules-install-exec-hook: log4j-copy-jar jest-copy-jar
	$(mkinstalldirs) $(JAVA_MOD_DST_DIR)
	cp $(MOD_JARS) $(JAVA_MOD_DST_DIR)

java-modules-uninstall-exec-hook:
	rm -f $(JAVA_MODULES_INSTALLED_JARS)

java-modules-clean-hook:
	rm -rf $(abs_top_builddir)/modules/java-modules/*.log
	$(GRADLE) --project-cache-dir $(GRADLE_WORKDIR) -q -g $(GRADLE_WORKDIR) -p $(abs_top_srcdir)/modules/java-modules -PsyslogBuildDir=$(abs_top_builddir)/modules/java-modules -PsyslogDepsDir=$(abs_top_builddir)/modules/java/syslog-ng-core/libs clean
	rm -rf $(GRADLE_WORKDIR)


INSTALL_EXEC_HOOKS += java-modules-install-exec-hook
UNINSTALL_HOOKS += java-modules-uninstall-exec-hook
CLEAN_HOOKS += java-modules-clean-hook

endif

EXTRA_DIST += \
	modules/java-modules/common/build.gradle  \
	modules/java-modules/elastic/build.gradle \
	modules/java-modules/elastic-v2/build.gradle \
	modules/java-modules/kafka/build.gradle \
	modules/java-modules/hdfs/build.gradle    \
	modules/java-modules/dummy/build.gradle   \
	modules/java-modules/http/build.gradle   \
	modules/java-modules/settings.gradle \
	modules/java-modules/build.gradle \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/messageprocessor/ESMessageProcessor.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/messageprocessor/DummyProcessor.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/messageprocessor/ESBulkMessageProcessor.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/messageprocessor/ESMessageProcessorFactory.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/messageprocessor/ESSingleMessageProcessor.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/ElasticSearchDestination.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/client/ESTransportClient.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/client/ESClient.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/client/ESNodeClient.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/client/UnknownESClientModeException.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/client/ESClientFactory.java \
	modules/java-modules/elastic/src/main/java/org/syslog_ng/elasticsearch/ElasticSearchOptions.java \
	modules/java-modules/kafka/src/main/java/org/syslog_ng/KafkaDestination.java \
	modules/java-modules/kafka/src/main/java/org/syslog_ng/KafkaDestinationOptions.java \
	modules/java-modules/kafka/src/main/java/org/syslog_ng/KafkaDestinationProperties.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/logging/SyslogNgInternalLogger.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/InvalidOptionException.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/RequiredOptionDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/Option.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/TemplateOption.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/PortCheckDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/OptionDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/BooleanOptionDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/EnumOptionDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/Options.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/IntegerRangeCheckOptionDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/IntegerOptionDecorator.java \
	modules/java-modules/common/src/main/java/org/syslog_ng/options/StringOption.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestEnumOptionDecorator.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestRequiredOptionDecorator.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestStringOption.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestPortCheckDecorator.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestBooleanOptionDecorator.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestIntegerRangeCheckOptionDecorator.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestOption.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/options/test/TestIntegerOptionDecorator.java \
	modules/java-modules/common/src/test/java/org/syslog_ng/logging/test/MockLogDestination.java \
	modules/java-modules/hdfs/src/main/java/org/syslog_ng/hdfs/HdfsDestination.java \
	modules/java-modules/hdfs/src/main/java/org/syslog_ng/hdfs/HdfsOptions.java \
	modules/java-modules/http/src/main/java/org/syslog_ng/http/HTTPDestination.java \
	modules/java-modules/http/src/main/java/org/syslog_ng/http/HTTPDestinationOptions.java \
	modules/java-modules/dummy/src/main/java/org/syslog_ng/DummyTextDestination.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/ESIndex.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/ESMessageProcessor.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/esnative/ESNativeMessageProcessor.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/esnative/DummyProcessorNative.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/esnative/ESBulkNativeMessageProcessor.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/ESMessageProcessorFactory.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/esnative/ESSingleNativeMessageProcessor.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/ElasticSearchDestination.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/ESClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/esnative/ESTransportClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/esnative/ESNativeClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/esnative/ESNodeClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/UnknownESClientModeException.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/ESClientFactory.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/ElasticSearchOptions.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/esnative/ESTransportShieldClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/esnative/ESTransportSearchGuardClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/client/http/ESHttpClient.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/http/HttpBulkMessageProcessor.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/http/HttpMessageProcessor.java \
	modules/java-modules/elastic-v2/src/main/java/org/syslog_ng/elasticsearch_v2/messageprocessor/http/HttpSingleMessageProcessor.java
