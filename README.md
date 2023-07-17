# nginx-debug

Nginx container image with debug context, useful for k8s and Docker testing 🐋

Nginx parameters are captured using the nginx sub_filter declarations (see default.conf)

These parameters are then used within the customised index.html page

## Available on DockerHub

Prebuilt for arm64 and amd64 on DockerHub

```
docker pull spurin/nginx-debug
```

## Example usage (Kubernetes)

```
% kubectl run nginx-debug --image=spurin/nginx-debug 
pod/nginx-debug created

% kubectl get pod/nginx-debug -o wide
NAME          READY   STATUS    RESTARTS   AGE   IP          NODE       NOMINATED NODE   READINESS GATES
nginx-debug   1/1     Running   0          12s   10.42.1.3   worker-1   <none>           <none>

% curl 10.42.1.3
<!DOCTYPE html>
<body>
<p><em>Hostname: nginx-debug</em></p>
<p><em>IP Address: 10.42.1.3:80</em></p>
<p><em>URL: /</em></p>
<p><em>Request Method: GET</em></p>
<p><em>Request ID: bb1f86df8f291097fff8d64f8066df80</em></p>
</body>
</html>
```

## Example usage (Docker)

```
% docker run -d --name nginx-debug -p 8080:80 spurin/nginx-debug
f960519c7b5cde5210728a00187188c17050bcde984035db53a4339fd0e6ae80

% curl localhost:8080
<!DOCTYPE html>
<body>
<p><em>Hostname: f960519c7b5c</em></p>
<p><em>IP Address: 172.17.0.4:80</em></p>
<p><em>URL: /</em></p>
<p><em>Request Method: GET</em></p>
<p><em>Request ID: 14172c9352e8e09eae3c1b018f5e211b</em></p>
</body>
</html>
```
