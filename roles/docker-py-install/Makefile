PWD=$(shell pwd)
ROLE_NAME=docker-py-install
ROLE_PATH=/etc/ansible/roles/$(ROLE_NAME)
TEST_VERSION=ansible --version
TEST_SYNTAX=ansible-playbook -vv -i 'localhost,' -c local $(ROLE_PATH)/tests/main.yml --syntax-check
TEST_PLAYBOOK=ansible-playbook -vv -i 'localhost,' -c local $(ROLE_PATH)/tests/main.yml
TEST_CMD=$(TEST_VERSION); $(TEST_SYNTAX); $(TEST_PLAYBOOK)
TEST_IMAGE_UBUNTU_14=williamyeh/ansible:ubuntu14.04
TEST_IMAGE_UBUNTU_16=williamyeh/ansible:ubuntu16.04
TEST_IMAGE_CENTOS_7=williamyeh/ansible:centos7

.PHONY: test

ubuntu14.04-pull-image:
	docker image pull "$(TEST_IMAGE_UBUNTU_14)"

ubuntu16.04-pull-image:
	docker image pull "$(TEST_IMAGE_UBUNTU_16)"

centos7-pull-image:
	docker image pull "$(TEST_IMAGE_CENTOS_7)"

ubuntu14.04-test: ubuntu14.04-pull-image
	docker run --rm -e "ROLE_NAME=$(ROLE_NAME)" -v $(PWD):$(ROLE_PATH) "$(TEST_IMAGE_UBUNTU_14)" /bin/bash -c "$(TEST_CMD)"

ubuntu16.04-test: ubuntu16.04-pull-image
	docker run --rm -e "ROLE_NAME=$(ROLE_NAME)" -v $(PWD):$(ROLE_PATH) "$(TEST_IMAGE_UBUNTU_16)" /bin/bash -c "$(TEST_CMD)"

centos7-test: centos7-pull-image
	docker run --rm -e "ROLE_NAME=$(ROLE_NAME)" -v $(PWD):$(ROLE_PATH) "$(TEST_IMAGE_CENTOS_7)" /bin/bash -c "$(TEST_CMD)"

test: ubuntu16.04-test ubuntu14.04-test centos7-test
