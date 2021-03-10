# TransactionReceipt

## TransactionReceipt

The summary of a transaction’s result so far. If the transaction has not reached consensus, this result will be necessarily incomplete.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>status</code>
      </td>
      <td style="text-align:left"><a href="responsecode.md#responsecodeenum">ResponseCodeEnum</a>
      </td>
      <td style="text-align:left">The consensus status of the transaction; is UNKNOWN if consensus has not
        been reached, or if the associated transaction did not have a valid payer
        signature</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>accountID</code>
      </td>
      <td style="text-align:left"><a href="../basic-types/accountid.md">AccountID</a>
      </td>
      <td style="text-align:left">In the receipt of a CryptoCreate, the id of the newly created account</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>fileID</code>
      </td>
      <td style="text-align:left"><a href="../basic-types/fileid.md">FileID</a>
      </td>
      <td style="text-align:left">In the receipt of a FileCreate, the id of the newly created file</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>contractID</code>
      </td>
      <td style="text-align:left"><a href="../basic-types/contractid.md">ContractID</a>
      </td>
      <td style="text-align:left">In the receipt of a ContractCreate, the id of the newly created contract</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>exchangeRate</code>
      </td>
      <td style="text-align:left"><a href="exchangerate.md#exchangerateset">ExchangeRateSet</a>
      </td>
      <td style="text-align:left">The exchange rates in effect when the transaction reached consensus</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>topicID</code>
      </td>
      <td style="text-align:left"><a href="../basic-types/topicid.md">TopicID</a>
      </td>
      <td style="text-align:left">In the receipt of a ConsensusCreateTopic, the id of the newly created
        topic.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>topicSequenceNumber</code>
      </td>
      <td style="text-align:left">uint64</td>
      <td style="text-align:left">In the receipt of a ConsensusSubmitMessage, the new sequence number of
        the topic that received the message</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>topicRunningHash</code>
      </td>
      <td style="text-align:left">bytes</td>
      <td style="text-align:left">
        <p></p>
        <p>In the receipt of a ConsensusSubmitMessage, the new running hash of the
          topic that received the message. This 48-byte field is the output of a
          particular SHA-384 digest whose input data are determined by the value
          of the topicRunningHashVersion. Please see table below.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>topicRunningHashVersion</code>
      </td>
      <td style="text-align:left">uint64</td>
      <td style="text-align:left">In the receipt of a ConsensusSubmitMessage, the version of the SHA-384
        digest used to update the running hash.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>tokenID</code>
      </td>
      <td style="text-align:left"><a href="../basic-types/tokenid.md">TokenID</a>
      </td>
      <td style="text-align:left">In the receipt of a CreateToken, the id of the newly created token</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>scheduleID</code>
      </td>
      <td style="text-align:left"><a href="../basic-types/scheduleid.md">ScheduleID</a>
      </td>
      <td style="text-align:left">In the receipt of a CreateSchedule, the id of the newly created Scheduled
        Entity</td>
    </tr>
  </tbody>
</table>

#### Topic Running Hash 

The input data to the SHA-384 digest in order.

<table>
  <thead>
    <tr>
      <th style="text-align:left">topicRunningHashVersion</th>
      <th style="text-align:left">Input data to the SHA-384 digest in order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">0 or 1</td>
      <td style="text-align:left">
        <p>1. The previous running hash of the topic (48 bytes)</p>
        <p>2. The topic&apos;s shard (8 bytes)</p>
        <p>3. The topic&apos;s realm (8 bytes)</p>
        <p>4. The topic&apos;s number (8 bytes)</p>
        <p>5. The number of seconds since the epoch before the ConsensusSubmitMessage
          reached consensus (8 bytes)</p>
        <p>6. The number of nanoseconds since 5. before the ConsensusSubmitMessage
          reached consensus (4 bytes)</p>
        <p>7. The topicSequenceNumber from above (8 bytes)</p>
        <p>8. The message bytes from the ConsensusSubmitMessage (variable).</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">2</td>
      <td style="text-align:left">
        <p>1. The previous running hash of the topic (48 bytes)</p>
        <p>2. The topicRunningHashVersion below (8 bytes)</p>
        <p>3. The topic&apos;s shard (8 bytes)</p>
        <p>4. The topic&apos;s realm (8 bytes)</p>
        <p>5. The topic&apos;s number (8 bytes)</p>
        <p>6. The number of seconds since the epoch before the ConsensusSubmitMessage
          reached consensus (8 bytes)</p>
        <p>7. The number of nanoseconds since 6. before the ConsensusSubmitMessage
          reached consensus (4 bytes)</p>
        <p>8. The topicSequenceNumber from above (8 bytes)</p>
        <p>9. The output of the SHA-384 digest of the message bytes from the consensusSubmitMessage
          (48 bytes)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">3</td>
      <td style="text-align:left">
        <p>1. The previous running hash of the topic (48 bytes)</p>
        <p>2. The topicRunningHashVersion below (8 bytes)</p>
        <p>3. The payer account&apos;s shard (8 bytes)</p>
        <p>4. The payer account&apos;s realm (8 bytes)</p>
        <p>5. The payer account&apos;s number (8 bytes)</p>
        <p>6. The topic&apos;s shard (8 bytes)</p>
        <p>7. The topic&apos;s realm (8 bytes)</p>
        <p>8. The topic&apos;s number (8 bytes)</p>
        <p>9. The number of seconds since the epoch before the ConsensusSubmitMessage
          reached consensus (8 bytes)</p>
        <p>10. The number of nanoseconds since 9. before the ConsensusSubmitMessage
          reached consensus (4 bytes)</p>
        <p>11. The topicSequenceNumber from above (8 bytes)</p>
        <p>12. The output of the SHA-384 digest of the message bytes from the consensusSubmitMessage
          (48 bytes)</p>
      </td>
    </tr>
  </tbody>
</table>



