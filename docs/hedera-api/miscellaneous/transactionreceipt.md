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
      <td style="text-align:left">status</td>
      <td style="text-align:left"><a href="responsecode.md#responsecodeenum">ResponseCodeEnum</a>
      </td>
      <td style="text-align:left">The consensus status of the transaction; is UNKNOWN if consensus has not
        been reached, or if the associated transaction did not have a valid payer
        signature</td>
    </tr>
    <tr>
      <td style="text-align:left">accountID</td>
      <td style="text-align:left"><a href="../basic-types/accountid.md">AccountID</a>
      </td>
      <td style="text-align:left">In the receipt of a CryptoCreate, the id of the newly created account</td>
    </tr>
    <tr>
      <td style="text-align:left">fileID</td>
      <td style="text-align:left"><a href="../basic-types/fileid.md">FileID</a>
      </td>
      <td style="text-align:left">In the receipt of a FileCreate, the id of the newly created file</td>
    </tr>
    <tr>
      <td style="text-align:left">contractID</td>
      <td style="text-align:left"><a href="../basic-types/contractid.md">ContractID</a>
      </td>
      <td style="text-align:left">In the receipt of a ContractCreate, the id of the newly created contract</td>
    </tr>
    <tr>
      <td style="text-align:left">exchangeRate</td>
      <td style="text-align:left"><a href="exchangerate.md#exchangerateset">ExchangeRateSet</a>
      </td>
      <td style="text-align:left">The exchange rates in effect when the transaction reached consensus</td>
    </tr>
    <tr>
      <td style="text-align:left">topicID</td>
      <td style="text-align:left"><a href="../basic-types/topicid.md">TopicID</a>
      </td>
      <td style="text-align:left">In the receipt of a ConsensusCreateTopic, the id of the newly created
        topic.</td>
    </tr>
    <tr>
      <td style="text-align:left">topicSequenceNumber</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">In the receipt of a ConsensusSubmitMessage, the new sequence number of
        the topic that received the message</td>
    </tr>
    <tr>
      <td style="text-align:left">topicRunningHash</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p></p>
        <p>In the receipt of a ConsensusSubmitMessage, the new running hash of the
          topic that received the message. This 48-byte field is the output of a
          particular SHA-384 digest whose input data are determined by the value
          of the topicRunningHashVersion below. The bytes of each uint64 or uint32
          are to be in Big-Endian format.</p>
        <ol>
          <li>The previous running hash of the topic (48 bytes)</li>
          <li>The topic&apos;s shard (8 bytes)</li>
          <li>The topic&apos;s realm (8 bytes)</li>
          <li>The topic&apos;s number (8 bytes)</li>
          <li>The number of seconds since the epoch before the ConsensusSubmitMessage
            reached consensus (8 bytes)</li>
          <li>The number of nanoseconds since 5. before the ConsensusSubmitMessage reached
            consensus (4 bytes)</li>
          <li>The topicSequenceNumber from above (8 bytes)</li>
          <li>The message bytes from the ConsensusSubmitMessage (variable).</li>
          <li>The previous running hash of the topic (48 bytes)</li>
          <li>The topicRunningHashVersion below (8 bytes)</li>
          <li>The topic&apos;s shard (8 bytes)</li>
          <li>The topic&apos;s realm (8 bytes)</li>
          <li>The topic&apos;s number (8 bytes)</li>
          <li>The number of seconds since the epoch before the ConsensusSubmitMessage
            reached consensus (8 bytes)</li>
          <li>The number of nanoseconds since 6. before the ConsensusSubmitMessage reached
            consensus (4 bytes)</li>
          <li>The topicSequenceNumber from above (8 bytes)</li>
          <li>The output of the SHA-384 digest of the message bytes from the consensusSubmitMessage
            (48 bytes)</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">topicRunningHashVersion</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">In the receipt of a ConsensusSubmitMessage, the version of the SHA-384
        digest used to update the running hash.</td>
    </tr>
  </tbody>
</table>

