# CKAD Reference Doc

This document contains a list of all the important exam detail, study material and reference document needed to prepare yourself for the CKAD exam.

## TL;DR
The 4 main key ingredients to clear the exam are:
- Understanding of the K8s concepts
- Knowing imperative commands to create objects in K8s
- Ability to handle yaml files in an editor
- Typing Speed 

To get better with all these, you just have to PRACTICE, there is no escape here. And once you get comfortable then go for the test.

## Exam Specifications
1. Number of Questions: 19
2. Total time given: 2hrs.
3. Exam type: Lab based, no multiple choice questions
4. References allowed: all K8s domain docs are allowed 

## Courses
1. If you are starting out with Kubernetes, then I would highly recommend [this course](https://www.udemy.com/course/learn-kubernetes/) by Mumshad Mannambeth. All the concepts are nicely explained and comes with quizzes and labs that would help you clear your basics.
2. This is recommended course by Mumshad Mannambeth on [CKAD with Practice Tests](https://www.udemy.com/course/certified-kubernetes-application-developer/), covers all the topic for the CKAD exam.
 It comes unlimited access to questions and labs and will be sufficient to clear the exam if done properly.

## Aliases and Environment Variables
I can not emphasize more on the importance of setting aliases:
```
    1. alias k="kubectl"
    2. alias kgp="k get pods"
    3. alias kd="k describe"
    4. alias kc="k create -f"
    5. alias kdel="k delete -f"
    6. alias kns="k config set-context --current --namespace"
```
You can also create environment variables for the most used flags

```
    1. export do="--dry-run=client -o yaml"  # to get the object in yaml format, example: kgp nginx $do
   
    2. export del="--grace-period=0 --force" # delete the object instantly, k delete pod nginx $del
```

## Vim Settings
Since you have to play with YAMLs, it is better to have a familiar settings, something like this
```
$ vi ~/.vimrc
set nu
set ic
set et
set sw=2
set ts=2
```

## Most widely used imperative commands
To be able to successfully clear the test you have to stay away from YAMLs as much as possible and this is where the imperative commands comes in handy.
1. Create namespace named production
```
$ k create namespace production 
```
2. Get all namespace
```
$ k get namespace
```
3. Get pods from all namespaces
```
$ kgp -A 
```
4. Get the name of the current namespace
```
$ kd pods | grep -i namespace -m 1
```
5. Output the nginx deploy object in yaml and store it a file
```
$ k get deploy nginx $do > nginx-deploy.yaml
```
6. Create a object using a yaml file
```
$ kcc nginx.yaml
```
7. Delete the object created in the above step
```
$ kdd nginx.yaml
```
8. Delete the same object without any delay
```
$ kdd nginx.yaml $del
```
9. Describe the nginx pod
```
$ kd pod nginx
```
10. Create configmap prodconfig in the current namespace
```
$ k create cm prodconfig --from-literal=key1=value1
```

<details>
  <summary> Click to continue with imperative commands!</summary>
  
  11. Create secret named prodsecret
  ```sql
  $ k create secret generic prodsecret --from-literal=key2=value2 
  ```

  12. Create a nginx pod and expose its port 80 on the container
  ```
  $ k run nginx --image=nginx --port=80
  ```

  13. Create a deploy nginx with 3 replicas
  ```
  $ k create deploy nginx --image=nfinx --replicas=3
  ```
 
 14. Expose the deployment created above with a ClusterIP service
 ```
 $ k expose deploy nginx --port=80 --target-port=8000 # ClusterIP service is the default type when you create a service like this
 ```
 
 15. Generate a yaml for a deployment without creating it
 ```
 $ k create deploy nginx --image=nginx --replicas=15 $do
 ```
 
 16. Get the names of nodes running the pods
 ```
 $ kgp -o wide
 ```

 17. Get the nodes
 ```
 $ k get nodes -o wide
 ```

 18. Run a nginx pod with command 'sleep 3600'
 ```
 $ k run nginx --image=nginx -- /bin/sh -c 'sleep 3600'
 ```
 
 19. Get into a running nginx pod and run command 'ls'
 ```
 $ k exec nginx -it -- /bin/sh
  ls
 ```
 
</details>


## Practice Material
There are several options available here but I would recommend doing as many questions as many times as you can
1. Git Repo with scenario questions: https://github.com/dgkanatsios/CKAD-exercises
2. Another good resource: https://codeburst.io/kubernetes-ckad-weekly-challenges-overview-and-tips-7282b36a2681 by Kim Wuestkamp
3. 150 Question set available [here](https://medium.com/bb-tutorials-and-thoughts/practice-enough-with-these-questions-for-the-ckad-exam-2f42d1228552)

## My Exam Experience

Some observations from my exam:
- You can start the exam 15 mins before the schedule time, so starting early does help because some time it takes long time to complete pre-requisite checks like ID, env, etc.
 
- I skipped the questions which had less than 3% weightage with a long description, you can always flag them and come back later to solve it

- While preparing for this test I bookmarked all the important topic which turned out to be a huge plus when giving the exam 

- The tips for creating aliases helped me complete the exam in ~50 mins and go over the flagged questions once again

- This exam is all about getting 66%, so you don't have attempt all the questions. Make sure whatever you do is correct at least 66% worth of points