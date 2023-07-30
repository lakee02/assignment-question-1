1. In the title of the header, it displays 5 orders but there are 6 orders in the table. We want to display the total number of orders in the header title.
<HeaderTitle primaryTitle="Orders" secondaryTitle="6 orders" />
Before it was 5 order in Dashboard.jsx

2. In the table order submitted date is missing, we have timestamp data included in the src\assets\timeStamps.json with the corresponding ids, please combine that with the order data and make sure the order submitted date is being displayed in the table

i copy the timestamp object from timeStamps.json and paste into data.json result object 
"timestamps": {
        "orderReceived": "2022-11-04T15:29:00Z",
        "orderStatusUpdated": "2022-11-04T15:29:00Z",
        "orderSubmitted": "2022-11-04T15:29:00Z"
      }

3. Order Volume cell is displaying USD values, can you please make it display the currency value selected on the dropdown located in the header of the dashboard

sol.
I pass the currency as a prop from Dashboard.jsx to List.jsx
<List rows={mockData.results} currency={currency} />

const List = ({ rows ,currency}) => {
  return (
    <table className={styles.container}>
      <thead>
        <ListHeader>
          <ListHeaderCell>Order ID</ListHeaderCell>
          <ListHeaderCell>Buy/Sell</ListHeaderCell>
          <ListHeaderCell>Country</ListHeaderCell>
          <ListHeaderCell>Order Submitted</ListHeaderCell>
        <ListHeaderCell>Order Volume / {currency}</ListHeaderCell>  // here i am set the currency replce with USD
        </ListHeader>
      </thead>
      <tbody>
        {rows.map((row) => (
          <ListRow>
            <ListRowCell>{row["&id"]}</ListRowCell>
            <ListRowCell>{row.executionDetails.buySellIndicator}</ListRowCell>
            <ListRowCell>{row.executionDetails.orderStatus}</ListRowCell>
            <ListRowCell>{row.timestamps.orderSubmitted}</ListRowCell>
            <ListRowCell>{row.bestExecutionData.orderVolume[currency]}</ListRowCell> // previously here .USD but i use currency as a value.
          </ListRow>
        ))}
      </tbody>
    </table>
  );
};