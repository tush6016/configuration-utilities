pipeline {
    agent {label 'eks'}

    stages {
        stage('Configuration') {
            steps {
                script {
                    sh 'cd'
                    sh 'sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo'
                    sh 'sudo yum -y install terraform'
                    sh 'curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.9/aws-iam-authenticator_0.5.9_linux_amd64'
                    sh 'chmod +x ./aws-iam-authenticator'
                    sh "echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc"
                    sh 'curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"'
                    sh 'sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl'
                    sh 'curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp'
                    sh 'sudo mv -v /tmp/eksctl /usr/local/bin'
                    sh 'eksctl version'
                }
            }
        }
    }
}
