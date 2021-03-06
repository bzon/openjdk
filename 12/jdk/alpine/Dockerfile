FROM alpine:3.8

ENV JAVA_HOME /opt/openjdk-12
ENV PATH $JAVA_HOME/bin:$PATH

# http://jdk.java.net/
ENV JAVA_VERSION 12-ea+14
ENV JAVA_URL https://download.java.net/java/early_access/alpine/14/binaries/openjdk-12-ea+14_linux-x64-musl_bin.tar.gz
ENV JAVA_SHA256 172c7d7c6859253822e03f0839f83627ffe06055f118423c6ef619a1af836b4c
# "For Alpine Linux, builds are produced on a reduced schedule and may not be in sync with the other platforms."

RUN set -eux; \
	\
	wget -O /openjdk.tgz "$JAVA_URL"; \
	echo "$JAVA_SHA256 */openjdk.tgz" | sha256sum -c -; \
	mkdir -p "$JAVA_HOME"; \
	tar --extract --file /openjdk.tgz --directory "$JAVA_HOME" --strip-components 1; \
	rm /openjdk.tgz; \
	\
# https://github.com/docker-library/openjdk/issues/212#issuecomment-420979840
# http://openjdk.java.net/jeps/341
	java -Xshare:dump; \
	\
# basic smoke test
	java --version; \
	javac --version

# https://docs.oracle.com/javase/10/tools/jshell.htm
# https://docs.oracle.com/javase/10/jshell/
# https://en.wikipedia.org/wiki/JShell
CMD ["jshell"]
