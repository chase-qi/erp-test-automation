BUILD_NUM = # retrieve latest build by default
BUILD_ENV = staging # alternately, use stable

provision-and-run-blue-zone: roles
ifeq ($(strip $(BUILD_NUM)),)
	ansible-playbook -l blue-zone -e erp_debian_installer_environment=$(BUILD_ENV) main.yml
else
	ansible-playbook -l blue-zone -e erp_build_number=$(BUILD_NUM) -e erp_debian_installer_environment=$(BUILD_ENV) main.yml
endif

provision-blue-zone: roles
ifeq ($(strip $(BUILD_NUM)),)
	ansible-playbook -t provision -l blue-zone -e erp_debian_installer_environment=$(BUILD_ENV) main.yml
else
	ansible-playbook -t provision -l blue-zone -e erp_build_number=$(BUILD_NUM) -e erp_debian_installer_environment=$(BUILD_ENV) main.yml
endif

run-blue-zone: roles
ifeq ($(strip $(BUILD_NUM)),)
	ansible-playbook -t run_test -l blue-zone -e erp_debian_installer_environment=$(BUILD_ENV) main.yml
else
	ansible-playbook -t run_test -l blue-zone -e "{erp_build_number: $(BUILD_NUM)}" -e erp_debian_installer_environment=$(BUILD_ENV) main.yml
endif

roles:
	ansible-galaxy install -p roles -r requirements.yml

clean:
	rm -rf roles
