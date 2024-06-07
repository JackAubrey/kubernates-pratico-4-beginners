# on the node, where the POD will be located (node1 in our case):
DIRNAME="vol1"
mkdir -p /mnt/disk/$DIRNAME
chmod 777 /mnt/disk/$DIRNAME

# after you can apply files
kubectl apply -f my-pvc-dynamic.yaml
kubectl apply -f my-pv-using-dynamic-pvc.yaml
kubectl apply -f pod-pvc.yaml