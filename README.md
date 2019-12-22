# Push Notification com React-Native/ Expo
## Exemplo simples do envio de notificações PUSH utilizando o expo

<img src="https://braze-marketing-assets.s3.amazonaws.com/images/iOS12_1120x660_190325_133100.gif">

### 1 - Como vamos fazer push notifications em nosso app Expo ? 🤷‍ 
#### Bom como todos nós já sabemos, as notificações push são de muita importância para uso em app´s de lembretes, marketing, mensagens e por aí vai uma infinidade de utilizações. Mais o grande porém é que fazer essas coisas sempre foi algo muito chato, e cheios de falhas. A grande novidade é que parece que de um tempo pra cá essa dificuldade morreu, pois, hoje com a chegado do desenvolvimento de apps com react-native e expo as coisas começaram a caminhar para o lado mais fácil e simples.
#### Ok! então vamos ao que interessa, o expo possui uma função que tem acesso as propriedades de notificações do S.O seja ele android ou IOS, o que ele faz basicamente é gerar um token do dispositivo, esse token ele é basicamente uma chave primária para os celulares, ou seja cada celular tem seu token ( “ RG ” ) e esse token nunca muda. Blz então precisamos obter esse token do nosso dispositivo móvel, para isso devemos dar permissão de notificações em nosso dispositivo. isso é feito por uma função própria do expo, vou dar um exemplo e assim fica mais fácil. 
#### Bom dei um `expo init app-notifi` e voalá.
```
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});

```
#### Gerei meu código inicial padrão do expo, bom basicamente não vamos instalar nada, pois o expo ele já vem com alguns pacotes instalados, como é o caso das notifications. Bom sendo assim, vamos construir nossas funções de maneira simples e que possamos a partir disso criar nossas futuras aplicações. Vou montando função por função e no final junto tudo ok?

#### Então vamos importar nossas dependência para o funcionamento correto do expo-notifications
  ##### 1 - `import * as Permissions from 'expo-permissions';`
  ##### 2 - `import { Notifications } from 'expo';`

#### Ok! depois de importado isso, vamos chamar essas funções para que as mesmas possam começar a funcionar corretamente.
#### Dentro da nossa class vamos inserir nosso codigo
```
componentDidMount = async () => {

    //Funcao responsavel para montar o status de permissao para o envio de notificações 
    const { status: existingStatus } = await Permissions.getAsync(
      Permissions.NOTIFICATIONS
    );
    let finalStatus = existingStatus;
    if (existingStatus !== 'granted') {
      const { status } = await Permissions.askAsync(Permissions.NOTIFICATIONS);
      finalStatus = status;
    }
    
    //caso o finalStatus nao estiver liberado ou seja com granted, nao podera gerar o token de notificacaoes 
    if (finalStatus !== 'granted') {
      return;
    }
    
    //se todas as permissoes estiverem ok, sera gerado um token, que tem como objetivo a entrega das notificacoes 
    //unicamente para o dispositivo responsavel por pertencer a este token
    let token = await Notifications.getExpoPushTokenAsync();
    console.log( token );
  }
  
```

#### Enfim para facilitar, vou deixar aqui meu código completo do App.js 
##### app.js
```
import React,{ Component } from 'react';
import { StyleSheet, Text, View } from 'react-native';
import * as Permissions from 'expo-permissions';
import { Notifications } from 'expo';

export default class App extends Component {


        
  componentDidMount = async () => {
    const { status: existingStatus } = await Permissions.getAsync(
      Permissions.NOTIFICATIONS
    );
    let finalStatus = existingStatus;

    if (existingStatus !== 'granted') {
      const { status } = await Permissions.askAsync(Permissions.NOTIFICATIONS);
      finalStatus = status;
    }

    if (finalStatus !== 'granted') {
      return;
    }

    let token = await Notifications.getExpoPushTokenAsync();
    console.log( token );
  }
  
  render() {
    return (
      <View style={styles.container}>
        <Text>Open up App.js to start working on your app!</Text>
      </View>
    );
  };
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});


```
#### Beleza, agora vamos salvar o cod e rodar, se tudo deu muito certo, nosso `console.log(token);` vai mostrar o token gerado a partir do seu celular pessoal. Se você ver algo como isso ExponentPushToken[FaRGySNWuAhsKmE4UR3asD] siginifca que deu certo, ai para testar se realmente seu celular está recebendo notificações entre neste site da própria expo. 
<a href="https://expo.io/notifications">https://expo.io/notifications</a>
#### assim que você entrar no site faça o seguinte: 

