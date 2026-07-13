# **CONRADO'S QUEST**
<p align="center">
  <a href="https://asasgamedev.github.io/ConradosQuest/Documents/TDD">
    <img src="https://img.shields.io/badge/TDD-2563EB?style=for-the-badge" alt="TDD">
  </a>
  &nbsp;
  <a href="https://asasgamedev.github.io/ConradosQuest/">
    <img src="https://img.shields.io/badge/GDD-16A34A?style=for-the-badge" alt="GDD">
  </a>
  &nbsp;
  <a href="https://asasgamedev.github.io/ConradosQuest/Documents/GDD">
    <img src="https://img.shields.io/badge/Complete_GDD-7C3A?style=for-the-badge" alt="Complete GDD">
  </a>
   &nbsp;
  <a href="https://asasgamedev.github.io/ConradosQuest/Documents/DevLog/DevLogIndex">
    <img src="https://img.shields.io/badge/DevLog-16A3AA?style=for-the-badge" alt="Complete GDD">
  </a>
</p>

# **Event Bus**

## **Ficha técnica:**
- **`Arquiteturas`**: Observer.
- **`Objetivos`**: Sistema simples que cuida da auxiliar o sistema a se manter desacoplado e cuidar da entrega dos eventos a quem necessitar ouvir. 
- **`Depende de`**: NDA.
- **`Dependentes`**: NDA.

## **Lista de Classes:**
 - Classe estática EventBus

## **Descrição:**
O event Bus é um sistema simples que cuida da entrega de eventos, ele é desenvolvido de forma estática, e genérica, ou seja a cada chamado tipificado há a criação de uma "instância" nova, com uma lista da tipificação com os eventos delegados, que recebem desse estrutura.

## **Documentação de Uso:**
Existem quatros métodos publícos para consumo desse sistema, dois são os mais fundamentais, os de inscrição e o de remoção, aqui segue exemplos de chamados.

C# -
```csharp
    //Grava o método: MyMethod que tem como parametro uma struct MyStruct.
    EventBus<MyStruct>.Subscribe(MyMethod);
    //Remove o Método MyMethod para que não seja mais considerado no chamado.
    EventBus<MyStruct>.Unsubscribe(MyMethod);
```

Também é possível fazer o chamado, para cada um desses métodos através do chamado do Event Bus, passando uma estrutura do mesmo método.

C#
```Csharp
EventBus<MyStruct>.Call(myStructInstance);
```

Para facilitar chamados foi criado uma Task para que possa ser feito o chamado com um delay de forma a poder configurar melhor os chamados.

C#
```Csharp
EventBus<MyStruct>.CallDelayed(myStructInstance, 2f);
```

## Código completo:
Aqui segue o código completo dessa classe, como no jogo final.

<details>

<summary>Event Bus complete</summary>

```Csharp
using System.Collections.Generic;
using System.Threading.Tasks;

namespace Asas.Utility
{
    /// <summary>
    /// Event Class that deals with delivering a event to the correct destination.
    /// </summary>
    /// <typeparam name="T">The type of a struct.</typeparam>
    public static class EventBus<T> where T : struct
    {
        /// <summary>
        /// A list of the actions in the system.
        /// </summary>
        private static readonly HashSet<System.Action<T>> m_Events = new();

        /// <summary>
        /// Called to subscrive an event to be called by it type.
        /// </summary>
        /// <param name="action">the event to be called.</param>
        public static void Subscribe(System.Action<T> action) => m_Events.Add(action);

        /// <summary>
        /// The method to remove an event from being called.
        /// </summary>
        /// <param name="action">The event to be unsubscribed.</param>
        public static void Unsubscribe(System.Action<T> action) => m_Events.Remove(action);

        /// <summary>
        /// This is a method to call an event by it args.
        /// </summary>
        /// <param name="eventArgs">the arguments to be called.</param>
        public static void Call(T eventArgs)
        {
            var copy = new System.Action<T>[m_Events.Count];
            m_Events.CopyTo(copy);
            foreach (System.Action<T> action in copy)
            {
                action?.Invoke(eventArgs);
            }
        }

        /// <summary>
        /// Method to call a delayed event.
        /// </summary>
        /// <param name="eventArgs">the args to be called.</param>
        /// <param name="delayInSeconds">the delay to call it in seconds.</param>
        public static async Task CallDelayed(T eventArgs, int delayInSeconds)
        {
            await Task.Delay(1000 * delayInSeconds);
            Call(eventArgs);
        }
    }
}
```

</details>

### **Asas GameDev**
<a href="https://www.linkedin.com/in/thadeu-moscatelli-2559061b0/" target="_blank">
  <img src="https://img.icons8.com/color/48/linkedin.png" alt="LinkedIn" width="24" height="24">
</a>
&nbsp;
<a href="https://wa.me/5515997329328" target="_blank">
  <img src="https://api.iconify.design/logos/whatsapp-icon.svg" alt="WhatsApp" width="20" height="20">
</a>