# This file is generated by the template.

REGISTRY	?=lcr.loongnix.cn
ORGANIZATION	?=distroless
REPOSITORY	?=static-debian11
TAG		?=nonroot
LATEST		?=true

IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):$(TAG)
LATEST_IMAGE=$(REGISTRY)/$(ORGANIZATION)/$(REPOSITORY):latest
ROOTFS=$(REPOSITORY)-rootfs.tar
URL_PREFIX=http://cloud.loongnix.cn/releases/loongarch64/gcr/distroless

default: image

$(ROOTFS):
	no_proxy=$(no_proxy) wget $(URL_PREFIX)/$@ -O rootfs.tar

image: $(ROOTFS)
	docker build \
		--build-arg http_proxy=$(http_proxy) \
		--build-arg https_proxy=$(https_proxy) \
		--build-arg no_proxy='cloud.loongnix.cn' \
		-t $(IMAGE) \
		.

push:
	docker push $(IMAGE)
	#latest image
	@if [ $(LATEST) = "true" ]; \
		then \
		docker tag $(IMAGE) $(LATEST_IMAGE); \
		docker push $(LATEST_IMAGE); \
	fi
