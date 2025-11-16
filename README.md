docker build -t webapp:1.0 .
docker run -p 5000:5000 webapp:1.0



Steps i used for creating helm
============================================
CD KUBERNETES_PROJECT
# optional, just to keep things clean
mkdir helm
cd helm

# this generates a starter Helm chart
helm create webapp-python

change below in values.yaml
--------------------------------
replicaCount: 2
image:
  repository: keerthi973/webapp
  pullPolicy: Always
  tag: "latest"
service:
  type: NodePort
  port: 8080

below changes in gtemplates/deployment.yml
- name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag | default .Chart.AppVersion }}"
          imagePullPolicy: {{ .Values.image.pullPolicy }}
          env:
            - name: REDIS_HOST
              value: "redis-service"   # we'll create this later when we add Redis
          ports:
            - name: http
              containerPort: 5000
              protocol: TCP