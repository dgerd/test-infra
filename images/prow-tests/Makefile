# Copyright 2018 The Knative Authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

IMG = gcr.io/knative-tests/test-infra/prow-tests
TAG := $(shell date +v%Y%m%d)-$(shell git describe --always --dirty --match '^$$')

all: build

build:
	docker build -t $(IMG):$(TAG) -f Dockerfile ../..
	docker tag $(IMG):$(TAG) $(IMG):latest

push_versioned: build
	docker push $(IMG):$(TAG)

push_latest: build
	docker push $(IMG):latest

clean:
	rm -fr githubhelper dep-collector

push: push_versioned push_latest clean
