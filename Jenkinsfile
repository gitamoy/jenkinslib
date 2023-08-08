#!groovy
//@Libary('jeninslib@master') //加载共享库
@Library('jenlibkins') _

def tools = new org.devops.tools()


//String workspace = "/data/jenkins/workspace"

pipeline {
    //agent any
    agent { node { label "build01"  //指定运行节点的标签或者名称
                   // customWorkspace "${workspace}" //指定运行时工作目录（可选） 
    	}
    }
    
    options {
        timestamps();  //日志会有时间
        skipDefaultCheckout();  //删除隐式checkout scm语句
        disableConcurrentBuilds();  //禁止并行
        timeout(time: 1, unit: 'HOURS') //流水线超时设置1h
    }

    /*
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
    */
    stages {
        //下载代码
        stage("GetCode") {  //阶段名称
            steps{  //步骤
                timeout(time: 5, unit: "MINUTES"){  //步骤超时时间
                    script{  //运行的代码
                        println('获取代码')
                        tools.PrintMsg("This is my library!")
                    }
                }
            }
        }    
    }    


    //构建后操作
    post {
        // 总时执行
        always {
            script {
                println('always')
            }
        }    
        
        //成功后执行
        success {
            script {
                //currentBuild 全局变量
                //description  构建描述
                currentBuild.description += "\n 构建成功！"
            }
        }
    
        //失败后执行
        failure {
            script {
                currentBuild.description += "\n 构建失败！"
            }
        }
        
        //取消后执行
        aborted {
            script {
                currentBuild.description += "\n 构建取消！"
            }
        }    
    }
}
