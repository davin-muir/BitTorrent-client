#### BitTorrent Client
##### BitTorrent overview
BitTorrent is a peer-peer file sharing protocol in which data is transferred between a bundle of peers on the internet. Instead of files being distributed from a centralized server, data is downloaded/uploaded from multiple peers simultaneously, which reduces latency.
- The .torrent file moderates the integrity of file 'pieces', and the amount of pieces.
- BitTorrent Specification


##### .torrent files
BitTorrent clients are endpoints that implement the BitTorrent protocol, namely uTorrent, Tixati & Deluge. Each client has to read the file specifications (filename, file size, URL  & its source from the .torrent file (meta data). 
- Metadata values are encoded as bencode dictionaries, a binary format useful for distributing unstructured data.
- Bencode supports four data types:
	- byte strings
	- integers
	- lists 
	- dictionaries
- Bencoded data can easily be converted to JSON or object literals in Python.



##### Features
[x] Downloading pieces
[ ] Uploading pieces
[ ] Tests



##### Walkthrough
###### Bencoding:
- Encodes python objects to a sequence of loosley structured bytes.
- Decodes bencoded data to the corresponding python object.
###### TorrentClient:
- Connects to the tracker and retrieves available peers to initiate a connection.
- Creates a queue of active peers
- Moderates the order & amount of pieces to be requested from remote peers.
###### Communication
- Handles the downloading/uploaded of a torrent's pieces.
- Retrieves an available peer from the queue, attempts to open a connection, and perfoms a BitTorrent 'handshake' to the peer.
- Once the handshake is initiated, the endpoint cant request any more data from remote peers until a response is returned from the peer.
- If the connection drops, the endpoint moves on to the next available peer in the queue.
