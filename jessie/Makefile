.PHONY: all push

USER="501stalpha1"
ifeq ($(shell uname -m), i686)
  PLATFORM="386"
else
  PLATFORM="amd64"
endif
SUITE="jessie"

all: .last-docker-build

.last-docker-build: Dockerfile
	docker build -t "$(USER)/buildpack-deps:$(SUITE)-$(PLATFORM)" .
	@touch $@

push: .last-docker-push

.last-docker-push: .last-docker-build
	docker push "$(USER)/buildpack-deps:$(SUITE)-$(PLATFORM)"
	manifest-tool push from-spec ./manifest.yml
	@touch $@
