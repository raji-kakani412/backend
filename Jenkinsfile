@Library('jenkins-shared-lib') _ 

def configMap=[
    project: "expense"
    component: "backend"
]

if(! env.BRANCH_NAME.equalsIgnoreCase('main')){ //true if branch is feature branch
    nodeJSEKSPipeline(configMap)
}
else{
    echo "Follow the process of PROD release"
}