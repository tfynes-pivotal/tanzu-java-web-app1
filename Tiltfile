load('.tanzu/tanzu_tilt_extensions.py', 'tanzu_k8s_yaml')


SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", default='harbor.homelab.fynesy.com/test/tjwa1-source')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')

custom_build('harbor.homelab.fynesy.com/test/tjwa1',
    "tanzu apps workload apply -f config/workload.yaml --live-update \
      --local-path " + LOCAL_PATH + " --source-image " + SOURCE_IMAGE + " --yes && \
    .tanzu/wait.sh tjwa1",
  ['pom.xml', './target/classes'],
  live_update = [
    sync('./target/classes', '/workspace/BOOT-INF/classes')
  ],
  skips_local_docker=True
)

tanzu_k8s_yaml('tjwa1', 'harbor.homelab.fynesy.com/test/tjwa1', './config/workload.yaml')
