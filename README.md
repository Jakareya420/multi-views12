import { useState } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

export default function YouTubeMultiTab() {
  const [urls, setUrls] = useState([]);
  const [inputUrl, setInputUrl] = useState("");

  const addVideo = () => {
    if (inputUrl.trim() !== "") {
      setUrls([...urls, inputUrl]);
      setInputUrl("");
    }
  };

  const removeVideo = (index) => {
    setUrls(urls.filter((_, i) => i !== index));
  };

  return (
    <div className="p-6">
      <div className="flex gap-2 mb-4">
        <Input
          value={inputUrl}
          onChange={(e) => setInputUrl(e.target.value)}
          placeholder="YouTube ভিডিওর লিংক দিন"
        />
        <Button onClick={addVideo}>Add</Button>
      </div>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {urls.map((url, index) => {
          const videoId = new URL(url).searchParams.get("v");
          return (
            <Card key={index}>
              <CardContent className="p-2">
                <iframe
                  width="100%"
                  height="200"
                  src={`https://www.youtube.com/embed/${videoId}`}
                  frameBorder="0"
                  allowFullScreen
                ></iframe>
                <Button
                  variant="destructive"
                  className="mt-2"
                  onClick={() => removeVideo(index)}
                >
                  Remove
                </Button>
              </CardContent>
            </Card>
          );
        })}
      </div>
    </div>
  );
}
