
All Openshift command 

oc get pods 
oc get pod <name> -n <name_spece>



oc get cm common-config -o yaml


oc describe cm alertmanager-config  


oc get cm alertmanager-config   -o yaml | \
  sed -e 's|alertmanager.yml: * |alertmanager.yml: sfathii|'


oc get cm alertmanager-config -n jenkins-csb-hhadad  -o yaml | run 'sed' commands to make updates | oc create cm alertmanager-config --from-file=config/alertmanager/alertmanager.yml -n jenkins-csb-hhadad -o yaml --dry-run | oc apply -f - 


oc delete configmap alertmanager-config -n jenkins-csb-hhadad 
oc create configmap 
oc rollout latest alertmanager-main -n jenkins-csb-hhadad

oc get cm  -n  jenkins-csb-sfathii

oc patch cm myconfig -p $(cat patch_file.yaml)


# with paremter
oc patch cm patch-test -p "{"data": {"targets-jenkins.yml": "tom" }}"
oc patch cm patch-test -p "{\"data\": {\"targets-jenkins.yml\": \"${TOM}\" }}" 

# Patch to file 
; Work https://stackoverflow.com/questions/52536664/add-a-file-into-an-existing-openshift-configmap
➜  testComfigMap oc patch cm patch-test --patch-file targets-jenkins.yml

configmap/patch-test patched
➜  testComfigMap 
; File name fommat cat targets-jenkins.yml
data:
  targets-jenkins.yml: |
    - targets:
      - amq-broker-jenkins-csb-messaging-qe.apps.ocp-c1.prod.psi.redhat.com
      - atomic-qe-jenkins-csb-atomic-qe.apps.ocp4.prod.psi.redhat.com
      - auto-jenkins-csb-kniqe.apps.ocp-c1.prod.psi.redhat.com




oc patch cm patch-test -p '''{"data": {"targets-jenkins.yml": "$(cat targets-jenkins.yml)" }}''' 
oc patch cm patch-test -p "{'data': {'targets-jenkins.yml': '$(cat targets-jenkins.yml)' }}" 

oc patch cm patch-test -p $(cat targets-jenkins.yml)






; https://stackoverflow.com/questions/52536664/add-a-file-into-an-existing-openshift-configmap
; oc patch dc test-deploy -p '{"spec": {"template": {"spec": {"containers": [{"name": "my-second-image","ports": [{"containerPort": 9090,"protocol": "TCP"}]}]}}}}'