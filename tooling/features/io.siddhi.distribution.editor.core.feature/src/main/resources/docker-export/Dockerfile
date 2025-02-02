# ------------------------------------------------------------------------
#
# Copyright 2019 WSO2, Inc. (http://wso2.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License
#
# ------------------------------------------------------------------------

# use siddhi-runner-base
FROM siddhiio/siddhi-runner-base-alpine:{{PRODUCT_VERSION}}
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

ARG HOST_BUNDLES_DIR=./bundles
ARG HOST_JARS_DIR=./jars
ARG HOST_APPS_DIR=./siddhi-files
ARG JARS=${RUNTIME_SERVER_HOME}/jars
ARG BUNDLES=${RUNTIME_SERVER_HOME}/bundles
ARG APPS=${RUNTIME_SERVER_HOME}/deployment/siddhi-files
ARG CONFIG_FILE=./configurations.yaml
ARG CONFIG_FILE_PATH=${HOME}/configurations.yaml

# copy bundles & jars to the siddhi-runner distribution
COPY --chown=siddhi_user:siddhi_io ${HOST_APPS_DIR}/ ${APPS}
{{JARS_BLOCK}}
{{BUNDLES_BLOCK}}
{{CONFIGURATION_BLOCK}}

{{ENV_BLOCK}}

# expose ports
EXPOSE 9090 9443 9712 9612 7711 7611 7070 7443

RUN bash ${RUNTIME_SERVER_HOME}/bin/install-jars.sh

STOPSIGNAL SIGINT

ENTRYPOINT ["/home/siddhi_user/init.sh" {{CONFIGURATION_PARAMETER_BLOCK}}]
