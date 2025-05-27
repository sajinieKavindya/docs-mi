# Apache Pulsar Connector Reference

The following operations allow you to work with the Apache Pulsar Connector. Click an operation name to see parameter details and samples on how to use it.

---

To use the Apache Pulsar connector, add the <pulsar.init> element in your configuration before any other Apache Pulsar operation. This contains the connection parameters required to connect to Apache Pulsar. This can be with or without security depending on your requirements.

??? note "PULSAR"
    This operation allows you to initialize the connection to Apache Pulsar.
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>name</td>
            <td>Unique name to identify the connection by.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>serviceUrl</td>
            <td>The Pulsar broker URL to connect. It follows the format- pulsar://<host_name>:<port> where pulsar is the protocol. The content following the :// is the host name and the port on which the broker is running.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <th colspan="3">Additional parameters for connection</td>
        <tr>
            <td>connectionTimeoutMs</td>
            <td>Timeout for establishing a connection (in milliseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>operationTimeoutSeconds</td>
            <td>Timeout for client operations (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>requestTimeoutMs</td>
            <td>Timeout for requests (in milliseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>lookupTimeoutMs</td>
            <td>Timeout for lookup requests (in milliseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>connectionMaxIdleSeconds</td>
            <td>Maximum idle time for connections (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>numIoThreads</td>
            <td>Number of IO threads for Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>numListenerThreads</td>
            <td>Number of listener threads for Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>enableBusyWait</td>
            <td>Enable busy-wait for IO threads.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>initialBackoffIntervalNanos</td>
            <td>Initial backoff interval for reconnection attempts (in nanoseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxBackoffIntervalNanos</td>
            <td>Maximum backoff interval for reconnection attempts (in nanoseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>connectionsPerBroker</td>
            <td>Number of connections per broker.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>concurrentLookupRequest</td>
            <td>Number of concurrent lookup requests allowed.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxConcurrentLookupRequests</td>
            <td>Maximum number of concurrent lookup requests allowed on each broker connection.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxLookupRequests</td>
            <td>Maximum number of lookup requests allowed on each broker connection.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxLookupRedirects</td>
            <td>Maximum number of lookup redirects allowed.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxNumberOfRejectedRequestPerConnection</td>
            <td>Maximum number of rejected requests per connection.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>useTcpNoDelay</td>
            <td>Enable TCP no delay for network connections.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>enableTransaction</td>
            <td>Enable transaction support in Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>keepAliveIntervalSeconds</td>
            <td>Keep-alive interval for broker connections (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>statsIntervalSeconds</td>
            <td>Interval for statistics collection (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>memoryLimitBytes</td>
            <td>Memory limit for Pulsar client (in bytes).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>listenerName</td>
            <td>Listener name for the Pulsar client.</td>
            <td>No</td>
        </tr>
    </table>

??? note "PULSARSECURE"
    This operation allows you to initialize a secure and authorized connection to Apache Pulsar.
    <table>
        <tr>
            <th>Parameter Name</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
        <tr>
            <td>name</td>
            <td>Unique name to identify the connection by.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <td>serviceUrl</td>
            <td>The Pulsar broker URL to connect. It follows the format- pulsar+ssl://<host_name>:<port> where pulsar is the protocol and +ssl is an optional parameter that shows that the connection is secured by TLS. The content following the :// is the host name and the port on which the broker is running.</td>
            <td>Yes</td>
        </tr>
        <tr>
            <th colspan="3">Additional parameters for connection</td>
        <tr>
            <td>connectionTimeoutMs</td>
            <td>Timeout for establishing a connection (in milliseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>operationTimeoutSeconds</td>
            <td>Timeout for client operations (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>requestTimeoutMs</td>
            <td>Timeout for requests (in milliseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>lookupTimeoutMs</td>
            <td>Timeout for lookup requests (in milliseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>connectionMaxIdleSeconds</td>
            <td>Maximum idle time for connections (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>numIoThreads</td>
            <td>Number of IO threads for Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>numListenerThreads</td>
            <td>Number of listener threads for Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>enableBusyWait</td>
            <td>Enable busy-wait for IO threads.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>initialBackoffIntervalNanos</td>
            <td>Initial backoff interval for reconnection attempts (in nanoseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxBackoffIntervalNanos</td>
            <td>Maximum backoff interval for reconnection attempts (in nanoseconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>connectionsPerBroker</td>
            <td>Number of connections per broker.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>concurrentLookupRequest</td>
            <td>Number of concurrent lookup requests allowed.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxConcurrentLookupRequests</td>
            <td>Maximum number of concurrent lookup requests allowed on each broker connection.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxLookupRequests</td>
            <td>Maximum number of lookup requests allowed on each broker connection.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxLookupRedirects</td>
            <td>Maximum number of lookup redirects allowed.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>maxNumberOfRejectedRequestPerConnection</td>
            <td>Maximum number of rejected requests per connection.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>useTcpNoDelay</td>
            <td>Enable TCP no delay for network connections.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>enableTransaction</td>
            <td>Enable transaction support in Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>keepAliveIntervalSeconds</td>
            <td>Keep-alive interval for broker connections (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>statsIntervalSeconds</td>
            <td>Interval for statistics collection (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>memoryLimitBytes</td>
            <td>Memory limit for Pulsar client (in bytes).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>listenerName</td>
            <td>Listener name for the Pulsar client.</td>
            <td>No</td>
        </tr>
        <tr>
            <th colspan="3">Parameters for secure connection (TLS encryption)</td>
        <tr>
            <td>tlsAllowInsecureConnection</td>
            <td>Allow insecure TLS connections.</td>
            <td>No</td>
        </tr>        
        <tr>
            <td>tlsTrustCertsFilePath</td>
            <td>Path to the TLS trust certificates file.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>tlsTrustStorePath</td>
            <td>Path to the TLS trust store.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>tlsTrustStoreType</td>
            <td>Type of the TLS trust store.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>tlsTrustStorePassword</td>
            <td>Password for the TLS trust store.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>tlsProtocols</td>
            <td>List of enabled TLS protocols.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>tlsCiphers</td>
            <td>List of enabled TLS ciphers.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>autoCertRefreshSeconds</td>
            <td>Interval for automatic certificate refresh (in seconds).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>enableTlsHostnameVerification</td>
            <td>Enable hostname verification for TLS connections.</td>
            <td>No</td>
        </tr>
        <tr>
            <td>useKeyStoreTls</td>
            <td>Enable TLS using keystore.</td>
            <td>No</td>
        </tr>
        <tr>
            <th colspan="3">Parameters for Authorization</td>
        <tr>
            <td>authorizationType</td>
            <td>Type of authorization (e.g., JWT, TLS, OAUTH2, NONE).</td>
            <td>No</td>
        </tr>
        <tr>
            <td>jwtToken</td>
            <td>JWT token to be used with JWT authorization type.</td>
            <td>No</td>
        </tr>
    </table>

    **Sample configuration**

    Given below is a sample configuration to create a client connection without security.

    ```xml
    <pulsar.init>
        <name>pulsarConnection</name>
        <serviceUrl>pulsar://localhost:6650</serviceUrl>
        <connectionTimeoutMs>10000</connectionTimeoutMs>
        <operationTimeoutSeconds>30</operationTimeoutSeconds>
        <requestTimeoutMs>30000</requestTimeoutMs>
        <lookupTimeoutMs>10000</lookupTimeoutMs>
        <connectionMaxIdleSeconds>60</connectionMaxIdleSeconds>
        <numIoThreads>4</numIoThreads>
        <numListenerThreads>2</numListenerThreads>
        <enableBusyWait>true</enableBusyWait>
        <initialBackoffIntervalNanos>1000000</initialBackoffIntervalNanos>
        <maxBackoffIntervalNanos>1000000000</maxBackoffIntervalNanos>
        <connectionsPerBroker>1</connectionsPerBroker>
        <concurrentLookupRequest>10</concurrentLookupRequest>
        <maxConcurrentLookupRequests>100</maxConcurrentLookupRequests>
        <maxLookupRequests>1000</maxLookupRequests>
        <maxLookupRedirects>5</maxLookupRedirects>
        <maxNumberOfRejectedRequestPerConnection>100</maxNumberOfRejectedRequestPerConnection>
        <useTcpNoDelay>true</useTcpNoDelay>
        <enableTransaction>false</enableTransaction>
        <keepAliveIntervalSeconds>30</keepAliveIntervalSeconds>
        <statsIntervalSeconds>60</statsIntervalSeconds>
        <memoryLimitBytes>104857600</memoryLimitBytes>
        <listenerName>pulsarListener</listenerName>
    </pulsar.init>
    ```

---