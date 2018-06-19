
- Autoscaling
	
	https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

	>>> Fazer deployment
	$ kubectl run php-apache --image=gcr.io/google_containers/hpa-example --requests=cpu=200m --expose --port=80

	>>> Configurar autoscaling
	$ kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=20

	>>> Mostrar status do autoscaling
	$ kubectl get hpa

	>>> Gerar carga - container
	$ kubectl run -i --tty load-generator --image=busybox /bin/sh

	>>> Gerar carga - script
	$ while true; do wget -q -O- http://php-apache.default.svc.cluster.local; done


- Liveness

	https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/

	http.HandleFunc("/healthz", func(w http.ResponseWriter, r *http.Request) {
	    duration := time.Now().Sub(started)
	    if duration.Seconds() > 10 {
	        w.WriteHeader(500)
	        w.Write([]byte(fmt.Sprintf("error: %v", duration.Seconds())))
	    } else {
	        w.WriteHeader(200)
	        w.Write([]byte("ok"))
	    }
	});


	$ kubectl create -f https://k8s.io/docs/tasks/configure-pod-container/http-liveness.yaml

	Depois de 10 segundos, verificamos que o container reiniciou.

	$ kubectl describe pod liveness-http

	$ kubectl get pod liveness-http


- Rolling update
	https://kubernetes.io/docs/tasks/run-application/rolling-update-replication-controller/#updating-the-container-image

	$ kubectl apply -f rolling-update.yml

	Agora iremos fazer o upgrade da imagem de 1.7.9 para 1.9.1

	$ kubectl rolling-update my-nginx --image=nginx:1.9.1

	Vamos ver no dashboard e no console, o Kubernetes fazendo o upgrade das imagens, mantendo o serviço, e sempre 5 pods rodando. Está sendo feito 1 a 1.


- Jobs
	https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs

	$ kubectl create -f cronjob.yaml

	$ kubectl get cronjob hello

	$ kubectl get jobs --watch

	$ kubectl delete cronjob hello


>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

Se não coletar métricas, reiniciar o HEAPSTER e INFLUXDB, E KUBE-DNS

