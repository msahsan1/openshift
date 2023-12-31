<pre>
apiVersion: v1
items:
- apiVersion: image.openshift.io/v1
  kind: ImageStream
  metadata:
    annotations:
      openshift.io/generated-by: OpenShiftNewApp
    creationTimestamp: null
    labels:
      app: nginx
      app.kubernetes.io/component: nginx
      app.kubernetes.io/instance: nginx
    name: nginx
  spec:
    lookupPolicy:
      local: false
    tags:
    - annotations:
        openshift.io/imported-from: bitnami/nginx
      from:
        kind: DockerImage
        name: bitnami/nginx
      generation: null
      importPolicy:
        importMode: Legacy
      name: latest
      referencePolicy:
        type: ""
  status:
    dockerImageRepository: ""
- apiVersion: apps/v1
  kind: Deployment
  metadata:
    annotations:
      image.openshift.io/triggers: '[{"from":{"kind":"ImageStreamTag","name":"nginx:latest"},"fieldPath":"spec.template.spec.containers[?(@.name==\"nginx\")].image"}]'
      openshift.io/generated-by: OpenShiftNewApp
    creationTimestamp: null
    labels:
      app: nginx
      app.kubernetes.io/component: nginx
      app.kubernetes.io/instance: nginx
    name: nginx
  spec:
    replicas: 1
    selector:
      matchLabels:
        deployment: nginx
    strategy: {}
    template:
      metadata:
        annotations:
          openshift.io/generated-by: OpenShiftNewApp
        creationTimestamp: null
        labels:
          deployment: nginx
      spec:
        containers:
        - image: ' '
          name: nginx
          ports:
          - containerPort: 8080
            protocol: TCP
          - containerPort: 8443
            protocol: TCP
          resources: {}
  status: {}
- apiVersion: v1
  kind: Service
  metadata:
    annotations:
      openshift.io/generated-by: OpenShiftNewApp
    creationTimestamp: null
    labels:
      app: nginx
      app.kubernetes.io/component: nginx
      app.kubernetes.io/instance: nginx
    name: nginx
  spec:
    ports:
    - name: 8080-tcp
      port: 8080
      protocol: TCP
      targetPort: 8080
    - name: 8443-tcp
      port: 8443
      protocol: TCP
      targetPort: 8443
    selector:
      deployment: nginx
  status:
    loadBalancer: {}
kind: List
metadata: {}
</pre>

