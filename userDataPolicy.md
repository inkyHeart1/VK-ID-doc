# Настройка модального окна с политикой конфиденциальности и передаваемыми данными

Когда пользователь авторизуется на сайте через кнопку VK ID, под кнопкой авторизации отображается модальное окно с политикой конфиденциальности и передаваемыми данными.

Для настройки отображения модального окна используется метод `Connect.userDataPolicy`.

## Сигнатура метода

```typescript
Connect.userDataPolicy(uuid: string): VKDataPolicyResult
```

## Описание параметров

В данном методе используется всего один параметр — `uuid`. Уникальная строка, генерируемая на стороне `DataPolicyEventsSDK`, которая далее передается во всех запросах.

## Возвращаемое значение

Метод возвращает объект `VKDataPolicyResult`.

Представление объекта `VKDataPolicyResult`:

  ```typescript
  interface VKDataPolicyResult {
    show: () => Promise<any>;
    hide: () => void;
    destroy: () => void;
  }
  ```

Описание объекта: 

  - `show` — показать модальное окно;
  - `hide` — скрыть модальное окно;
  - `destroy` — удалить модальное окно.

## Особенности работы метода

После принятия пользовательского соглашения значение `uuid` передается в payload `VKDataPolicyPayload` для дальнейшей передачи в другие запросы.

Представление `VKDataPolicyPayload`:

```typescript
interface VKDataPolicyPayload {
    uuid: string;
    policyAccepted: boolean;
}
```

Описание `VKDataPolicyPayload`:

  - `uuid` — уникальная строка, полученная после принятия пользовательского соглашения;
  - `policyAccepted` — флаг принятия пользовательского соглашения.

## Пример реализации метода

Ниже представлен пример встраивания модального окна:

```typescript
Connect.userDataPolicy(uuid: '3422b448-2460-4fd2-9183-8000de6f8343')
 .show()
.then(() => {
 console.log('Policy was accepted');
 });
```
