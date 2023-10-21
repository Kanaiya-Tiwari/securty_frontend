import React, { useState, useEffect } from 'react';
import axios from 'axios';

const Admin = () => {
  const [transactions, setTransactions] = useState([]);

  useEffect(() => {
    // Fetch transactions from the backend
    axios.get('http://localhost:5000/transactions')
      .then(response => {
        setTransactions(response.data);
      })
      .catch(error => {
        console.log(error);
      });
  }, []);

  return (
    <div>
      <h1>Admin Interface</h1>
      <h2>Transaction History</h2>
      <table>
        <tbody>
          <tr>
            <th>Sender</th>
            <th>Recipient</th>
            <th>Amount</th>
            <th>Timestamp</th>
          </tr>
          {transactions.map(transaction => (
            <tr key={transaction.timestamp}>
              <td>{transaction.senderId}</td>
              <td>{transaction.recipientId}</td>
              <td>{transaction.amount}</td>
              <td>{transaction.timestamp}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default Admin;
