## Application Service > Maps > Error Codes

## API Error Codes
|resultCode|	resultMessage| Description | Remarks |
|:---:|:---:|:---:|:---:|
|0|	|Successful| Common |
|100|Result Not Found| No result is available | Search Only |
|101|Argument Error| /Error in parameter | Common |
|102|Internal Server Error|Error in server| Search Only |
|201|	Searching for Security| POI	security facilities | Search Only |
|202|	Longitude/Latitude |Longitude/Latitude| Search Only |
|203|	Mobile Phone Number|Mobile phone number| Search Only |
|204|	Invalid Query|Other errors in input range| Search Only
|205|	POI not in given Admin| No result is available (Region setting)|Search Only|
|206|	POI not in given Area|No result is available (Area setting)|Search Only|
|207|	POI not in given Category|No result is available (Classification setting)|Search Only|
|208|	Neighbor Search Only|No result is available (Enter nearby search only)|Search Only|
|209|	Neighbor Search not Found|(No search result available for nearby +keyword)|Search Only|
|300|	AppKey Error|Error in appkey authentication|Common|
|501|	Unknown Fail|Failed (unknown)|For search only|
|502|	Apply Smart Re-navigation|Apply Smart Re-navigation|Navigation only|
|503|	Canceled navigation by user | User canceled navigation |Navigation only|
|504|	Error due to Checksum | Error due to Checksum |Navigation only|
|517|	Memory allocation failure | Memory allocation failure |Navigation only|
|518|	File open failure | Failed to open the file |Navigation only|
|519|	File read failure| Failed to read the file |Navigation only|
|520|	File write failure| Failed to write the file |Navigation only|
|521|	Socket connection failure |Failed to connect the socket|Navigation only|
|532|	Request parameter is invalid | Invalid request parameter |Navigation only|
|533|	The starting point is not selected, or the wrong starting point |The starting point is invalid or not selected|Navigation only|
|534|	Destination is not selected or wrong destination |Destination is invalid or not selected|Navigation only|
|535|	Wrong stopover |Invalid stopover|Navigation only|
|536|	Link Projection failure | Link Projection |Navigation only|
|537|	Exceeding the navigational distance (1000km, walking navigation: 20km) | Exceeds the navigational distance (1000km, walking navigation: 20km) |Navigation only|
|538|	Exceeds the number of expandable nodes | Exceeds the number of expandable nodes |Navigation only|
|539|	Expansion failure | Failed to expand |Navigation only|
|540|	Expansion failure due to inactivity or traffic control | Failed to expand due to special circumstances or traffic control |Navigation only|
|541|	Expansion failure due to vehicle height/weight restrictions near the starting point | Failed to expand due to vehicle height/weight restrictions near the starting point |Navigation only|
|542|	Expansion failed due to a part-time curfew near the departure point | Failed to expand due to limited curfew near the departure point |Navigation only|
|543|	The destination is a physical island road, and there are no established ferry routes. | The destination is a road on a physical island, and there are no ferry routes available. |Navigation only|
|544|	The departure or destination is a logical (transportation) island, and there are more than one destination |The starting point or destination is a logical (transportation) island, and there is more than one destination |Navigation only|
|545| No data requested | No data requested |Navigation only|
