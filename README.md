# docu3c

import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';

class KidLocation extends StatefulWidget {
  final LatLng kidLocation;

  KidLocation({required this.kidLocation});

  @override
  _KidLocationState createState() => _KidLocationState();
}

class _KidLocationState extends State<KidLocation> {
  late GoogleMapController mapController;

  final LatLng _center = LatLng(45.521563, -122.677433);

  void onMapCreated(GoogleMapController controller) {
    mapController = controller;
    controller.animateCamera(CameraUpdate.newLatLng(widget.kidLocation));
  }

  @override
  Widget build(BuildContext context) {
    return GoogleMap(
      onMapCreated: onMapCreated,
      initialCameraPosition: CameraPosition(target: _center, zoom: 11.0),
      markers: Set<Marker>.of([
        Marker(
          markerId: MarkerId('kid'),
          position: widget.kidLocation,
          infoWindow: InfoWindow(
            title: 'Kid Location',
          ),
        ),
      ]),
    );
  }
}
