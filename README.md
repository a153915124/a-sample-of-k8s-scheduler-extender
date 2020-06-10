# sample-scheduler-extender

在示例https://github.com/tjrone/sample-scheduler-extender的基础上，修改业务逻辑，令0-4的节点随机数中非3的节点加入

```go

func LuckyPredicate(pod *v1.Pod, node v1.Node) (bool, []string, error) {\
	// 节点随机产生0-4的随机数，若随机数不等于3则成功fit
	lucky := rand.Intn(5) != 3
	if lucky {
		log.Printf("pod %v/%v is lucky to fit on node %v\n", pod.Name, pod.Namespace, node.Name)
		return true, nil, nil
	}
	log.Printf("pod %v/%v is unlucky to fit on node %v\n", pod.Name, pod.Namespace, node.Name)
	return false, []string{LuckyPredFailMsg}, nil
}
```