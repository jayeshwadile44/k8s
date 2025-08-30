# 1️⃣ Create a ReplicationController (RC) from YAML
kubectl create -f replication-controller.yaml
# → Creates an RC that launches pods as per the specified replica count.

# 2️⃣ Update RC after changing replicas or container image
kubectl apply -f replication-controller.yaml
# → Reconciles changes like replicas: 3 → 5. This applies the updated config to the RC.

# 3️⃣ Check RC and pods status
kubectl get replicationcontroller         # Shows RC with desired/current/ready pods
kubectl get pods                          # Lists all pods (RC/RS/others)

# 🧠 Note: RC error you faced
# Error: unknown field "spec.containers"
# → This means `containers` field was misplaced. It should be under:
# → spec.template.spec.containers (not directly under spec)

# 4️⃣ Create a ReplicaSet (RS) using YAML
kubectl create -f replicasets.yaml
# → ReplicaSet is a modern alternative to RC, used by Deployments internally.

# 5️⃣ Scale the ReplicaSet by editing YAML
# → Step 1: Edit replicasets.yaml, change:
#     replicas: 3 → replicas: 7
# → Step 2: Apply the updated YAML
kubectl apply -f replicasets.yaml

# 6️⃣ Confirm ReplicaSet and pod scaling
kubectl get replicaset                    # Shows RS with updated replica count
kubectl get pods                          # Verifies new pods are Running
kubectl get all                           # Lists all resources: pods, RC, RS, services

# 🔁 Optional: Scale RS without editing YAML
kubectl scale rs myapp-replicaset --replicas=7
# → Instantly scales without touching YAML (good for one-off/manual scaling)

# 🧠 Tip: Apply with save-config if you plan to use kubectl apply later
kubectl create --save-config -f replicasets.yaml

Welcome
