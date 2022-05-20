## User issue [#18506](https://github.com/Azure/azure-sdk-for-js/issues/18506)

### Steps to run the sample that uses ServiceBusAdministrationClient

1. Clone this project
2. `npm install` in this folder to install all the dependencies
3. Create `.env` file and populate it with `SERVICEBUS_CONNECTION_STRING` and `QUEUE_NAME` in it as shown in `sample.env`
4. Install `ts-node` globally (to be able to run the typescript file directly)
   > `npm install ts-node -g`
5. Running the sample with `ts-node adminClient.ts` in this folder should give you the following output.

```sh
C:\<path>\service-bus-18506>ts-node adminClient.ts

Created queue with name -  sample-queue
(Current)max delivery count =  10
(Updated)max delivery count =  12
Number of messages in the queue =  0
Name of the namespace -  <namespace-name>
Queue sample-queue has been deleted

```

The sample uses updateQueue method along with the createQueue and getQueue methods, they all work fine.

```ts
const getQueueResponse = await serviceBusAdministrationClient.getQueue(
  queueName
);
console.log(
  "(Current)max delivery count = ",
  getQueueResponse.maxDeliveryCount
);

getQueueResponse.maxDeliveryCount = 12;
const updateQueueResponse = await serviceBusAdministrationClient.updateQueue(
  getQueueResponse
);
console.log(
  "(Updated)max delivery count = ",
  updateQueueResponse.maxDeliveryCount
);
```

The response from the getQueue method is modified and passed as an argument to the updateQueue method.
