This repository is made for the DexCheck team.

Here you will find various graphQL queries for BitQuery.

There are instructions in every folder for the respective queries.


Please be aware that some queries will take different time to give back results than others. This is based on the volume of requested data.

==========================================================

General query instructions and syntax.

=========================

Networks:

In order to fetch result for the desired network, parameter after "network:" field must be changed respectively as follows:

ethereum(network:bsc) for Binance smart chain

ethereum(network:ethereum)  for Ethereum

ethereum(network:avalanche) for Avalanche

ethereum(network:matic) for Polygon

ethereum(network:fantom) for Fantom

ethereum(network:ethclassic) for Ethereum classic

ethereum(network:velas) for Velas

ethereum(network:klaytn) for Klaytn

ethereum(network:celo_baklava) for Celo


=========================

Filters:

=========================

Limits:

Currently bitquery don't accept more than 10000 results for 1 query.

"limit:" filter must be between 1 and 10000


Date:

Date format used in BitQuery is ISO8601
https://en.wikipedia.org/wiki/ISO_8601

Vanilla JS code to retrieve now time in ISO 8601 format:

var now = new Date().toISOString();




In "date:" - "since:" and "till:" additional filters can be applied for more precise results, one of them can be omitted (depends on desired results). 
date:{since: "ISO8601 time", till: "ISO8601 time"}


"asc:" stands for ascending order
"desc:" stands for descending order





