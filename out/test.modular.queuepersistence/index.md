Project: /_project.yaml
Book: /_book.yaml

# test.modular.queuepersistence


## **PROTOCOLS**

## QueuePersistenceTestService {:#QueuePersistenceTestService}
*Defined in [test.modular.queuepersistence/queue_persistence_test_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/modular/tests/queue_persistence_test_service.test.fidl#8)*


### GetMessageQueueToken {:#GetMessageQueueToken}

 Returns a sender token associated with the queue managed by this service.
 This token can be used to send messages to this queue.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message_queue_token</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>















