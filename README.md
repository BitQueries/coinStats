Total coin liquidity.


In order to get total liquidity in USD vale, there will be 3 queries involved.


1.Get the Liquidity pair for desired coin.

Query:


query  {  
  ethereum(network:bsc) {
    dexTrades(
      baseCurrency: {is:"` + COIN ADDRESS VARIABLE HERE + `"}
      options: {desc: "trades"}
    ) {
      poolToken: smartContract {
        address {
          address
        }
      }
     trades:count
    }
  }
}


"baseCurrency:" - This is the desired coin address.
Example - if you want to get Pancake liquidity pair, you must insert the Cake token address.

Store the liquidity address in array for further proceessing.

=================================================

2.Get the balances of the liquidity pair (BNB, USDT, BUSD, USDC).

Query:

{
  ethereum(network: bsc) {
    address(address: {is: "` + COIN ADDRESS VARIABLE HERE + `"}) {
      balances(currency: {in: ["0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c", "0xe9e7cea3dedca5984780bafc599bd69add087d56",
	  "0x55d398326f99059ff775485246999027b3197955","0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d"]}) {
        currency {
          symbol
		  address
        }
        value
      }
    }
  }
}


Store the balances in array for further processing.


=================================================


3.Get the current USD price for the respected liquidity token.

Query:


{
  ethereum(network: bsc) {
    dexTrades(
      options: {limit: 1, desc: "block.timestamp.time"}
	  date: {till: "` + CURRENT TIME IN ISO8601 FORMAT + `"}
      exchangeName: {in:  ["Pancake" "Pancake v2"]}
      baseCurrency: {is: "` + LIQUIDITY TOKEN VARIABLE HERE + `"}
      quoteCurrency: {is: "0x55d398326f99059ff775485246999027b3197955"}
    ) {
      
      block {
        timestamp {
          time(format: "%Y-%m-%d %H:%M:%S")
        }
      }
      
      baseCurrency {
        symbol
        address
      }
      
      quoteCurrency {
        symbol
        address
      }
      
      quotePrice
    }
  }
}

Store the price in array and compare to previously stored data to get total liquidity USD value.

=================================================

4.General information


Get current time in ISO8601 format written in Vanilla JS:

var now = new Date().toISOString();



Frequent liquidity backup coins (BSC network):
WBNB - 0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c
BUSD - 0xe9e7cea3dedca5984780bafc599bd69add087d56
USDT - 0x55d398326f99059ff775485246999027b3197955
USDC - 0x8ac76a51cc950d9822d68b83fe1ad97b32cd580d


=================================================



