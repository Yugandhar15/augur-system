# augur-system
Augur system
import { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";

const mockDistributors = [
  {
    name: "Distributor A",
    shippedLastMonth: 1200,
    forecastNextMonth: 1350,
    ytdAverage: 1125,
    region: "North",
    status: "On Track",
  },
  {
    name: "Distributor B",
    shippedLastMonth: 980,
    forecastNextMonth: 1050,
    ytdAverage: 990,
    region: "East",
    status: "At Risk",
  },
  {
    name: "Distributor C",
    shippedLastMonth: 1500,
    forecastNextMonth: 1600,
    ytdAverage: 1475,
    region: "West",
    status: "On Track",
  },
];

export default function Dashboard() {
  const [distributors, setDistributors] = useState([]);

  useEffect(() => {
    // Simulate API call
    setTimeout(() => {
      setDistributors(mockDistributors);
    }, 500);
  }, []);

  return (
    <div className="min-h-screen bg-gray-100 p-6">
      <h1 className="text-3xl font-bold mb-6">Augur Distribution Dashboard</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {distributors.map((dist, idx) => (
          <Card key={idx} className="shadow-md rounded-2xl p-4 bg-white">
            <CardContent>
              <h2 className="text-xl font-semibold mb-2">{dist.name}</h2>
              <p className="text-sm text-gray-600 mb-1">Region: {dist.region}</p>
              <p className="text-sm text-gray-600 mb-1">Status: <span className={`font-semibold ${dist.status === "At Risk" ? "text-red-500" : "text-green-600"}`}>{dist.status}</span></p>
              <div className="my-4">
                <ResponsiveContainer width="100%" height={200}>
                  <BarChart data={[
                    { label: "Last Month", value: dist.shippedLastMonth },
                    { label: "Forecast", value: dist.forecastNextMonth },
                    { label: "YTD Avg", value: dist.ytdAverage }
                  ]}>
                    <XAxis dataKey="label" />
                    <YAxis />
                    <Tooltip />
                    <Bar dataKey="value" fill="#3b82f6" radius={[4, 4, 0, 0]} />
                  </BarChart>
                </ResponsiveContainer>
              </div>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
