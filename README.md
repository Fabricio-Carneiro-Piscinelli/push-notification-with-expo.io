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

