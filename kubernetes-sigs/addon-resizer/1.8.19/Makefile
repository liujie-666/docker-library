
REGISTRY?=lcr.loongnix.cn
ORGANIZATION?=kubernetes-sigs
REPOSITORY?=addon-resizer
TAG?=addon-resizer-1.8.19
LATEST?=true

GO_IMG?=lcr.loongnix.cn/library/golang:1.19

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(lastword $(subst -, ,$(TAG)))
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest

SOURCE_URL=https://github.com/kubernetes/autoscaler.git
SOURCE=$(shell echo $(SOURCE_URL) | awk -F '/' '{print $$NF}' | awk -F '.' '{print $$1}')
PATCH=0001-support-loong64.patch

default: image

src/$(SOURCE):
	git clone -b $(TAG) --depth=1 $(SOURCE_URL) $@
	cd $@ && \
		git apply ../../$(PATCH)

image: src/$(SOURCE)
	cd src/$(SOURCE)/addon-resizer && \
	ARCH=loong64 \
	BASEIMAGE=lcr.loongnix.cn/library/busybox:glibc \
	GO_IMG=$(GO_IMG) \
	IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY) \
		make container

push:
	docker push $(IMAGE)
	@if [ $(LATEST) = "true" ]; \
		then\
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi

clean:
	rm -rf src

