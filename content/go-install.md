Title: Instalando Go
Date: 2015-06-07 16:29
Modified: 2015-06-07 16:29
Category: Programação
Tags: Language, Programmer, Install, Go, Compile, Hello Word
Slug: instalando-go
Authors: Bleno Silva
Summary: Go Language

# Baixar e extrair no diretório /usr/local

    tar -C /usr/local -xzf go1.6.2.linux-amd64.tar.gz


# Exportar variável de ambiente

    echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc

# Teste sua instalação

Vamos criar um workspace no seguinte diretório $HOME/work

    mkdir -p ~/work/src/github.com/user/hello inside

Exportar variável de ambiente

    echo  'export GOPATH=$HOME/work' >> ~/.bashrc


Crie um arquivo chamdo hello.go no seguinte diretório ~/work/src/github.com/user/hello . 
Altere user para seu usuário do github

    vi ~/work/src/github.com/user/hello/hello.go

Colar o seguinte conteúdo no arquivo

    package main

    import "fmt"

    func main() {
        fmt.Printf("hello, world\n")
    }

E agora compilar

    go install github.com/user/hello

Então executar

    $GOPATH/bin/hello


Se você ver p "hello, word" , então sua instalação do GO está funcionando.

