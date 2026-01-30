# Basic Text, Icon and Button

import 'package:flutter/material.dart';

class Step15 extends StatefulWidget {
  const Step15({super.key});

  @override
  State<Step15> createState() => _Step15State();
}

class _Step15State extends State<Step15> {
  int suhu = 25;
  bool hujan = false;
  bool weekend = false;

  void plus() => setState(() => suhu++);
  void minus() => setState(() => suhu--);

  String get statusSuhu {
    if (suhu <= 18) return "Cold ❄️";
    if (suhu <= 28) return "Warm ☀️";
    return "Hot 🔥";
  }

  
  Recommendation get rekomendasi {
    
    if (hujan) {
      if (weekend) {
        return const Recommendation(
          icon: Icons.umbrella,
          title: "Better be doing indoor activities 🏠",
          subtitle: "Watch a mmovie, play video games and etc 🍿🎮",
        );
      } else {
        return const Recommendation(
          icon: Icons.umbrella,
          title: "Bring a raincoat and umbrella ☔",
          subtitle: "Do less other activities, do the nearby ones 🧥",
        );
      }
    }


    if (suhu <= 18) {
      if (weekend) {
        return const Recommendation(
          icon: Icons.ac_unit,
          title: "Perfect for a morning walk 🌄",
          subtitle: "Use light jacket 🧥",
        );
      } else {
        return const Recommendation(
          icon: Icons.ac_unit,
          title: "Perfect for morning jogging 🏃",
          subtitle: "Perfect weather 👟",
        );
      }
    } else if (suhu <= 28) {
      
      if (weekend) {
        return const Recommendation(
          icon: Icons.wb_cloudy,
          title: "Perfect for light exercise 🏃",
          subtitle: "Use normal clothes and shoes 👕👟",
        );
      } else {
        return const Recommendation(
          icon: Icons.wb_sunny,
          title: "Perfect less outdoor workout 🚶",
          subtitle: "Evening walk and shopping 🛍️",
        );
      }
    } else {
      
      if (weekend) {
        return const Recommendation(
          icon: Icons.wb_sunny,
          title: "Perfect for cool places 🧊",
          subtitle: "Find indoor cafes ☕",
        );
      } else {
        return const Recommendation(
          icon: Icons.local_drink,
          title: "Don't force to do a heavy workout 🥵",
          subtitle: "Finish drinking 🧃",
        );
      }
    }
  }

  @override
  Widget build(BuildContext context) {
    final rec = rekomendasi;

    return Scaffold(
      backgroundColor: const Color(0xFFBFE0FA),
      appBar: AppBar(
        title: const Text("Complex If-Else"),
        centerTitle: true,
        backgroundColor: Colors.deepOrange,
        foregroundColor: Colors.white,
      ),
      body: ListView(
        padding: const EdgeInsets.all(16),
        children: [
          const SizedBox(height: 6),
          const Text(
            "Activity Recommendation",
            style: TextStyle(fontSize: 28, fontWeight: FontWeight.bold),
          ),
          const SizedBox(height: 16),


          _card(
            child: Padding(
              padding: const EdgeInsets.all(16),
              child: Column(
                children: [
                  Row(
                    mainAxisAlignment: MainAxisAlignment.spaceBetween,
                    children: [
                      Text(
                        "Temperature: $suhu°C",
                        style: const TextStyle(
                          fontSize: 20,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                      Text(
                        statusSuhu,
                        style: const TextStyle(
                          fontSize: 18,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ],
                  ),
                  const SizedBox(height: 16),
                  Row(
                    children: [
                      Expanded(
                        child: ElevatedButton(
                          onPressed: minus,
                          style: ElevatedButton.styleFrom(
                            backgroundColor: Colors.white,
                            foregroundColor: Colors.blueGrey,
                            elevation: 0,
                            padding: const EdgeInsets.symmetric(vertical: 14),
                            shape: RoundedRectangleBorder(
                              borderRadius: BorderRadius.circular(30),
                              side: BorderSide(color: Colors.grey.shade300),
                            ),
                          ),
                          child: const Text(
                            "-",
                            style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
                          ),
                        ),
                      ),
                      const SizedBox(width: 14),
                      Expanded(
                        child: ElevatedButton(
                          onPressed: plus,
                          style: ElevatedButton.styleFrom(
                            backgroundColor: Colors.white,
                            foregroundColor: Colors.blueGrey,
                            elevation: 0,
                            padding: const EdgeInsets.symmetric(vertical: 14),
                            shape: RoundedRectangleBorder(
                              borderRadius: BorderRadius.circular(30),
                              side: BorderSide(color: Colors.grey.shade300),
                            ),
                          ),
                          child: const Text(
                            "+",
                            style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
                          ),
                        ),
                      ),
                    ],
                  ),
                ],
              ),
            ),
          ),

          const SizedBox(height: 16),


          _card(
            child: Column(
              children: [
                SwitchListTile(
                  title: const Text(
                    "Rain?",
                    style: TextStyle(fontWeight: FontWeight.bold),
                  ),
                  value: hujan,
                  onChanged: (v) => setState(() => hujan = v),
                ),
                const Divider(height: 1),
                SwitchListTile(
                  title: const Text(
                    "Weekend?",
                    style: TextStyle(fontWeight: FontWeight.bold),
                  ),
                  value: weekend,
                  onChanged: (v) => setState(() => weekend = v),
                ),
              ],
            ),
          ),

          const SizedBox(height: 20),


          _card(
            child: Padding(
              padding: const EdgeInsets.all(18),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.center,
                children: [
                  Icon(rec.icon, size: 90, color: Colors.orange),
                  const SizedBox(height: 16),
                  Text(
                    rec.title,
                    textAlign: TextAlign.center,
                    style: const TextStyle(
                      fontSize: 22,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  const SizedBox(height: 10),
                  Text(
                    rec.subtitle,
                    textAlign: TextAlign.center,
                    style: TextStyle(
                      fontSize: 16,
                      color: Colors.grey.shade700,
                      fontWeight: FontWeight.w600,
                    ),
                  ),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }

  Widget _card({required Widget child}) {
    return Container(
      decoration: BoxDecoration(
        color: const Color(0xFFF2F2F2),
        borderRadius: BorderRadius.circular(18),
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(0.12),
            blurRadius: 10,
            offset: const Offset(0, 4),
          ),
        ],
      ),
      child: child,
    );
  }
}

class Recommendation {
  final IconData icon;
  final String title;
  final String subtitle;

  const Recommendation({
    required this.icon,
    required this.title,
    required this.subtitle,
  });
}

