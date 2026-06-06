import React, { useState, useRef, useEffect } from 'react';
import { 
  Camera, 
  Upload, 
  Search, 
  Sparkles, 
  TrendingUp, 
  DollarSign, 
  Scale, 
  Plus, 
  Trash2, 
  Printer, 
  FileText, 
  RefreshCw, 
  AlertCircle, 
  HelpCircle,
  Tag,
  CheckCircle,
  Clock,
  Settings,
  X,
  Info
} from 'lucide-react';

// Setup environment and global variables
const appId = typeof __app_id !== 'undefined' ? __app_id : 'toybox-valuator-app';
const apiEndpoint = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent";

// High-Fidelity scalable SVG recreation of Buddy's Toys and Collectibles Sticker Logo
function BuddyLogo({ className = "h-16 w-auto" }) {
  return (
    <svg 
      viewBox="0 0 500 400" 
      className={`${className} transition-transform duration-200 hover:scale-105 filter drop-shadow-md`}
      xmlns="http://www.w3.org/2000/svg"
    >
      {/* Outer White Sticker Border Frame */}
      <rect 
        x="15" 
        y="45" 
        width="470" 
        height="310" 
        rx="68" 
        ry="68" 
        fill="#FFFFFF" 
      />
      
      {/* Main Vibrant Brand Orange Background */}
      <rect 
        x="25" 
        y="55" 
        width="450" 
        height="260" 
        rx="55" 
        ry="55" 
        fill="#FC4C02" 
      />

      {/* "BUDDY'S" Text with heavy white contour padding */}
      {/* Background White Contour Layer */}
      <text 
        x="250" 
        y="100" 
        textAnchor="middle" 
        fontFamily='system-ui, -apple-system, "Arial Black", "Impact", sans-serif' 
        fontWeight="900" 
        fontSize="56" 
        letterSpacing="1"
        fill="#FFFFFF"
        stroke="#FFFFFF"
        strokeWidth="16"
        strokeLinejoin="round"
        paintOrder="stroke fill"
      >
        BUDDY'S
      </text>
      {/* Foreground Blue Text Layer */}
      <text 
        x="250" 
        y="100" 
        textAnchor="middle" 
        fontFamily='system-ui, -apple-system, "Arial Black", "Impact", sans-serif' 
        fontWeight="900" 
        fontSize="56" 
        letterSpacing="1"
        fill="#2B59C3"
      >
        BUDDY'S
      </text>

      {/* "TOYS" Chunky Stylized Yellow Text with Heavy Black Outline */}
      {/* Background Black Outline Layer */}
      <text 
        x="250" 
        y="225" 
        textAnchor="middle" 
        fontFamily='"Arial Black", "Impact", "Trebuchet MS", sans-serif' 
        fontWeight="900" 
        fontSize="120" 
        letterSpacing="-3"
        fill="#1A1A1A"
        stroke="#1A1A1A"
        strokeWidth="28"
        strokeLinejoin="round"
        paintOrder="stroke fill"
      >
        TOYS
      </text>
      {/* Foreground Yellow Fill Layer */}
      <text 
        x="250" 
        y="225" 
        textAnchor="middle" 
        fontFamily='"Arial Black", "Impact", "Trebuchet MS", sans-serif' 
        fontWeight="900" 
        fontSize="120" 
        letterSpacing="-3"
        fill="#F6E71D"
      >
        TOYS
      </text>

      {/* "AND" Connective text */}
      {/* Background Black Outline Layer */}
      <text 
        x="250" 
        y="282" 
        textAnchor="middle" 
        fontFamily='"Arial Black", "Impact", sans-serif' 
        fontWeight="900" 
        fontSize="36" 
        letterSpacing="2"
        fill="#1A1A1A"
        stroke="#1A1A1A"
        strokeWidth="12"
        strokeLinejoin="round"
        paintOrder="stroke fill"
      >
        AND
      </text>
      {/* Foreground Yellow Layer */}
      <text 
        x="250" 
        y="282" 
        textAnchor="middle" 
        fontFamily='"Arial Black", "Impact", sans-serif' 
        fontWeight="900" 
        fontSize="36" 
        letterSpacing="2"
        fill="#F6E71D"
      >
        AND
      </text>

      {/* Bottom "COLLECTIBLES" Shield Base Container */}
      <rect 
        x="45" 
        y="290" 
        width="410" 
        height="80" 
        rx="40" 
        ry="40" 
        fill="#1A1A1D" 
        stroke="#FFFFFF" 
        strokeWidth="12"
      />
      
      {/* "COLLECTIBLES" Clean Sans-Serif Text */}
      <text 
        x="250" 
        y="342" 
        textAnchor="middle" 
        fontFamily='system-ui, -apple-system, "Arial Black", sans-serif' 
        fontWeight="800" 
        fontSize="34" 
        letterSpacing="5"
        fill="#FFFFFF"
      >
        COLLECTIBLES
      </text>
    </svg>
  );
}

export default function App() {
  // System states
  const [apiKey, setApiKey] = useState("");
  const [showKeyModal, setShowKeyModal] = useState(false);
  const [activeTab, setActiveTab] = useState("camera"); // 'camera' or 'search'
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  // Camera & Image states
  const [stream, setStream] = useState(null);
  const [cameraMode, setCameraMode] = useState("environment"); // 'user' or 'environment'
  const [capturedImage, setCapturedImage] = useState(null); // base64 data
  const [searchQuery, setSearchQuery] = useState("");
  const videoRef = useRef(null);

  // Evaluation results state
  const [evaluation, setEvaluation] = useState(null);
  
  // Consignment Calculator inputs (linked to current evaluation)
  const [listingPrice, setListingPrice] = useState(0);
  const [storeSplit, setStoreSplit] = useState(40); // Store gets 40%
  const [consignorSplit, setConsignorSplit] = useState(60); // Consignor gets 60%
  const [cleaningFee, setCleaningFee] = useState(0);
  const [processingFee, setProcessingFee] = useState(1.50);
  const [consignorName, setConsignorName] = useState("");
  const [itemCondition, setItemCondition] = useState("Very Good");

  // Ledger / Intake session state
  const [ledger, setLedger] = useState([]);
  const [filterStatus, setFilterStatus] = useState("all");

  // Step-by-step onboarding guide state
  const [showGuide, setShowGuide] = useState(false);

  // Initialize camera when tab is 'camera'
  useEffect(() => {
    if (activeTab === 'camera' && !capturedImage) {
      startCamera();
    } else {
      stopCamera();
    }
    return () => stopCamera();
  }, [activeTab, cameraMode, capturedImage]);

  // Handle calculation updates when listing price or splits change
  useEffect(() => {
    if (evaluation) {
      setListingPrice(evaluation.priceUsedAvg || 0);
    }
  }, [evaluation]);

  const startCamera = async () => {
    try {
      setError(null);
      if (stream) {
        stopCamera();
      }
      const constraints = {
        video: { facingMode: cameraMode, width: { ideal: 1280 }, height: { ideal: 720 } }
      };
      const mediaStream = await navigator.mediaDevices.getUserMedia(constraints);
      setStream(mediaStream);
      if (videoRef.current) {
        videoRef.current.srcObject = mediaStream;
      }
    } catch (err) {
      console.error("Camera access error:", err);
      setError("Unable to access camera. Please upload an image or type the toy name instead.");
      setActiveTab("search");
    }
  };

  const stopCamera = () => {
    if (stream) {
      stream.getTracks().forEach(track => track.stop());
      setStream(null);
    }
  };

  const switchCamera = () => {
    setCameraMode(prev => prev === "user" ? "environment" : "user");
  };

  const capturePhoto = () => {
    if (videoRef.current) {
      const canvas = document.createElement("canvas");
      canvas.width = videoRef.current.videoWidth;
      canvas.height = videoRef.current.videoHeight;
      const ctx = canvas.getContext("2d");
      ctx.drawImage(videoRef.current, 0, 0, canvas.width, canvas.height);
      const dataUrl = canvas.toDataURL("image/jpeg", 0.85);
      setCapturedImage(dataUrl);
      stopCamera();
    }
  };

  const handleFileUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => {
        setCapturedImage(reader.result);
        setError(null);
      };
      reader.readAsDataURL(file);
    }
  };

  const clearPhoto = () => {
    setCapturedImage(null);
    setEvaluation(null);
    if (activeTab === 'camera') {
      startCamera();
    }
  };

  // Exponential backoff runner for API requests
  const fetchWithRetry = async (url, options, retries = 5, delay = 1000) => {
    try {
      const response = await fetch(url, options);
      if (!response.ok) {
        throw new Error(`HTTP Error: ${response.status}`);
      }
      return await response.json();
    } catch (error) {
      if (retries > 0) {
        await new Promise(resolve => setTimeout(resolve, delay));
        return fetchWithRetry(url, options, retries - 1, delay * 2);
      }
      throw error;
    }
  };

  // Perform Gemini Evaluation
  const runEvaluation = async (isTextSearch = false) => {
    setLoading(true);
    setError(null);
    setEvaluation(null);

    // Build API Key logic
    const resolvedKey = apiKey || ""; // Empty string triggers standard preview environment configuration if available
    const url = `${apiEndpoint}?key=${resolvedKey}`;

    // Prompt structured strictly to request price ranges
    const systemPrompt = `You are an expert toy store appraiser and consignment consultant. 
Your goal is to inspect the provided input (image or description) and return accurate valuation metrics.
Strictly adhere to the following JSON schema response structure.
Estimate the values realistically based on current online platforms (like eBay, Mercari, and vintage toy databases).`;

    let payload = {};

    if (isTextSearch) {
      if (!searchQuery.trim()) {
        setError("Please enter a toy name or keyword first.");
        setLoading(false);
        return;
      }
      payload = {
        contents: [{
          parts: [{ 
            text: `Identify and value this toy: "${searchQuery}". Provide details on current brand-new MSRP, average used market pricing, and inspection notes.` 
          }]
        }]
      };
    } else {
      if (!capturedImage) {
        setError("Please snap or upload a photo first.");
        setLoading(false);
        return;
      }
      // Extract base64 clean data
      const base64Data = capturedImage.split(",")[1];
      payload = {
        contents: [{
          parts: [
            { text: "Analyze this toy image for consignment valuation. Provide: Name, Brand, Year, Estimated Retail/MSRP (New), Estimated Used Average Market Price (eBay), Key features, and current market demand." },
            { inlineData: { mimeType: "image/jpeg", data: base64Data } }
          ]
        }]
      };
    }

    // Add JSON configuration matching Schema
    payload.systemInstruction = { parts: [{ text: systemPrompt }] };
    payload.generationConfig = {
      responseMimeType: "application/json",
      responseSchema: {
        type: "OBJECT",
        properties: {
          toyName: { type: "STRING", description: "Standard official name of the toy" },
          brand: { type: "STRING", description: "Manufacturer or Brand (e.g., LEGO, Hasbro, Mattel, Funko)" },
          estimatedYear: { type: "STRING", description: "Year of release or approximate era" },
          priceNew: { type: "NUMBER", description: "Estimated original/current retail MSRP in USD" },
          priceUsedAvg: { type: "NUMBER", description: "Average used/resale price on eBay/secondary markets in USD" },
          priceUsedMin: { type: "NUMBER", description: "Lower range of secondary sales in USD" },
          priceUsedMax: { type: "NUMBER", description: "Higher range/collector value in USD" },
          confidenceScore: { type: "NUMBER", description: "Confidence of identification from 0 to 100" },
          demand: { type: "STRING", description: "High, Medium, or Low" },
          notes: { type: "STRING", description: "Summary of notable features, variants to look for, and condition warning flags." }
        },
        required: ["toyName", "brand", "priceNew", "priceUsedAvg", "demand"]
      }
    };

    try {
      const data = await fetchWithRetry(url, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload)
      });

      const responseText = data.candidates?.[0]?.content?.parts?.[0]?.text;
      if (!responseText) {
        throw new Error("No response content from model.");
      }

      const parsedResult = JSON.parse(responseText);
      setEvaluation(parsedResult);
    } catch (err) {
      console.error(err);
      setError("Valuation failed. The API may be busy or the request timed out. Please try again or refine your query.");
    } finally {
      setLoading(false);
    }
  };

  // Adjust splits safely
  const handleSplitChange = (val, source) => {
    const value = parseInt(val, 10);
    if (source === 'store') {
      setStoreSplit(value);
      setConsignorSplit(100 - value);
    } else {
      setConsignorSplit(value);
      setStoreSplit(100 - value);
    }
  };

  // Calculate detailed financial outputs
  const calculatePayouts = () => {
    if (!evaluation) return { storeShare: 0, consignorShare: 0, feesTotal: 0, netProfit: 0 };
    
    const grossSale = Number(listingPrice) || 0;
    const consignorBase = grossSale * (consignorSplit / 100);
    const storeBase = grossSale * (storeSplit / 100);
    
    // Cleaning fee paid by consignor out of their split, or processing fee added
    const fees = (Number(cleaningFee) || 0) + (Number(processingFee) || 0);
    
    const finalConsignorPayout = Math.max(0, consignorBase - fees);
    const finalStoreReturn = storeBase + fees;

    return {
      grossSale,
      consignorBase,
      storeBase,
      fees,
      finalConsignorPayout: finalConsignorPayout.toFixed(2),
      finalStoreReturn: finalStoreReturn.toFixed(2),
      consignorNet: finalConsignorPayout.toFixed(2),
      storeNetProfit: finalStoreReturn.toFixed(2)
    };
  };

  const financialMetrics = calculatePayouts();

  // Add evaluated toy to the active ledger session
  const addToLedger = () => {
    if (!evaluation) return;

    const newItem = {
      id: crypto.randomUUID(),
      toyName: evaluation.toyName,
      brand: evaluation.brand,
      consignor: consignorName || "Walk-in Customer",
      condition: itemCondition,
      suggestedRetail: evaluation.priceNew,
      marketAverage: evaluation.priceUsedAvg,
      agreedListingPrice: Number(listingPrice),
      consignorSplit: consignorSplit,
      storeSplit: storeSplit,
      consignorPayout: Number(financialMetrics.finalConsignorPayout),
      storeProfit: Number(financialMetrics.finalStoreReturn),
      date: new Date().toLocaleDateString(),
      status: "Active Draft", // "Active Draft", "Contract Approved", "Declined"
      image: capturedImage // Keep preview image reference in local ledger
    };

    setLedger(prev => [newItem, ...prev]);
    
    // Clear calculator state
    setConsignorName("");
    setItemCondition("Very Good");
    // Show visual confirmation or reset
    setEvaluation(null);
    setCapturedImage(null);
    setSearchQuery("");
    if (activeTab === 'camera') {
      startCamera();
    }
  };

  const updateLedgerStatus = (id, newStatus) => {
    setLedger(prev => prev.map(item => item.id === id ? { ...item, status: newStatus } : item));
  };

  const deleteLedgerItem = (id) => {
    setLedger(prev => prev.filter(item => item.id !== id));
  };

  const exportLedgerToCSV = () => {
    if (ledger.length === 0) return;
    
    const headers = ["Date", "Toy Name", "Brand", "Consignor Name", "Condition", "Market Price", "Listing Price", "Consignor Split %", "Consignor Payout ($)", "Store Profit ($)", "Status"];
    const rows = ledger.map(item => [
      item.date,
      `"${item.toyName.replace(/"/g, '""')}"`,
      `"${item.brand.replace(/"/g, '""')}"`,
      `"${item.consignor.replace(/"/g, '""')}"`,
      item.condition,
      item.marketAverage,
      item.agreedListingPrice,
      `${item.consignorSplit}%`,
      item.consignorPayout,
      item.storeProfit,
      item.status
    ]);

    const csvContent = "data:text/csv;charset=utf-8," 
      + [headers.join(","), ...rows.map(e => e.join(","))].join("\n");
    
    const encodedUri = encodeURI(csvContent);
    const link = document.createElement("a");
    link.setAttribute("href", encodedUri);
    link.setAttribute("download", `Toy_Consignment_Ledger_${new Date().toISOString().slice(0,10)}.csv`);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  // Filtered Ledger list
  const filteredLedger = ledger.filter(item => {
    if (filterStatus === "all") return true;
    return item.status.toLowerCase() === filterStatus.toLowerCase();
  });

  return (
    <div className="min-h-screen bg-slate-50 text-slate-800 font-sans flex flex-col antialiased">
      
      <header className="sticky top-0 z-40 bg-white border-b border-slate-200 shadow-sm">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex items-center justify-between">
          <div className="flex items-center space-x-3">
            {/* Scalable SVG representation of Buddy's Toys and Collectibles Logo */}
            <BuddyLogo className="h-16 w-auto sm:h-20" />
            <div className="hidden sm:block">
              <h1 className="text-lg font-black tracking-tight text-slate-900">
                BUDDY'S <span className="text-orange-600">CONSIGNMENT DESK</span>
              </h1>
              <p className="text-[10px] text-slate-500 font-bold uppercase tracking-wider">
                Official Valuation & Secondary Market Analyzer
              </p>
            </div>
          </div>

          <div className="flex items-center space-x-3">
            <button
              onClick={() => setShowGuide(true)}
              className="flex items-center space-x-1.5 px-3 py-1.5 rounded-lg border border-slate-200 text-slate-600 hover:bg-slate-50 text-sm font-medium transition"
            >
              <HelpCircle className="w-4 h-4 text-orange-500" />
              <span>How it Works</span>
            </button>
            
            <button
              onClick={() => setShowKeyModal(true)}
              className={`flex items-center space-x-1.5 px-3 py-1.5 rounded-lg text-sm font-medium transition ${
                apiKey ? 'bg-emerald-50 text-emerald-700 border border-emerald-200' : 'bg-slate-100 text-slate-700 border border-slate-200 hover:bg-slate-200'
              }`}
            >
              <Settings className="w-4 h-4" />
              <span>{apiKey ? "Custom API Connected" : "Custom Key Setup"}</span>
            </button>
          </div>
        </div>
      </header>

      {!apiKey && (
        <div className="bg-orange-50 border-b border-orange-200 text-orange-950 px-4 py-2 text-center text-sm flex items-center justify-center gap-2">
          <Info className="w-4 h-4 text-orange-600 shrink-0" />
          <span>Running in sandbox mode. Set up your Gemini API key for dedicated store inventory limits.</span>
          <button onClick={() => setShowKeyModal(true)} className="underline font-semibold hover:text-orange-950 ml-1">Setup Key</button>
        </div>
      )}

      {/* Main Workspace */}
      <main className="flex-1 max-w-7xl w-full mx-auto p-4 sm:p-6 lg:p-8 space-y-8">
        
        {/* Onboarding Guide Widget (Dismissible banner updated to orange/yellow palette) */}
        {!showGuide && (
          <div className="bg-gradient-to-r from-orange-600 via-orange-500 to-yellow-500 text-white rounded-2xl p-6 shadow-xl relative overflow-hidden">
            <div className="absolute top-0 right-0 p-8 opacity-10 pointer-events-none">
              <Camera className="w-40 h-40" />
            </div>
            <div className="relative z-10 max-w-3xl">
              <span className="bg-white/20 text-white px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider">Buddy's Store Companion Tool</span>
              <h2 className="text-2xl font-black mt-2">Instant Consignment Valuations powered by AI</h2>
              <p className="mt-2 text-white/95 text-sm sm:text-base leading-relaxed">
                Appraise toys instantly using our computer vision agent. Snap or upload a photo of any new or used toy, check live resale benchmarks from secondary markets like eBay, and calculate clean store-to-consignor profit splits!
              </p>
              <div className="mt-4 flex flex-wrap gap-3">
                <button 
                  onClick={() => setActiveTab("camera")}
                  className="bg-slate-900 text-white px-5 py-2.5 rounded-xl text-sm font-bold shadow-lg hover:bg-slate-800 transition active:scale-95"
                >
                  Start Live Scan
                </button>
                <button 
                  onClick={() => setShowGuide(true)}
                  className="bg-white/10 hover:bg-white/20 text-white border border-white/20 px-4 py-2 rounded-xl text-sm font-semibold transition"
                >
                  Learn Strategy
                </button>
              </div>
            </div>
          </div>
        )}

        <div className="grid grid-cols-1 lg:grid-cols-12 gap-8">
          
          {/* Left Column: Visual Capture & Inputs */}
          <div className="lg:col-span-5 space-y-6">
            <div className="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
              {/* Tab Selector */}
              <div className="flex border-b border-slate-100">
                <button
                  onClick={() => { setActiveTab("camera"); clearPhoto(); }}
                  className={`flex-1 flex items-center justify-center space-x-2 py-4 text-sm font-bold border-b-2 transition ${
                    activeTab === "camera" 
                      ? "border-orange-500 text-orange-600 bg-orange-50/20" 
                      : "border-transparent text-slate-500 hover:text-slate-800"
                  }`}
                >
                  <Camera className="w-4 h-4" />
                  <span>Use Camera / Upload</span>
                </button>
                <button
                  onClick={() => { setActiveTab("search"); clearPhoto(); }}
                  className={`flex-1 flex items-center justify-center space-x-2 py-4 text-sm font-bold border-b-2 transition ${
                    activeTab === "search" 
                      ? "border-orange-500 text-orange-600 bg-orange-50/20" 
                      : "border-transparent text-slate-500 hover:text-slate-800"
                  }`}
                >
                  <Search className="w-4 h-4" />
                  <span>Manual Lookup</span>
                </button>
              </div>

              {/* Tab: Camera/Upload Panel */}
              <div className="p-6">
                {activeTab === "camera" && (
                  <div className="space-y-4">
                    {/* Camera view or Captured image */}
                    {!capturedImage ? (
                      <div className="relative aspect-video w-full bg-slate-950 rounded-xl overflow-hidden shadow-inner flex flex-col items-center justify-center border-2 border-dashed border-slate-300">
                        {stream ? (
                          <video
                            ref={videoRef}
                            autoPlay
                            playsInline
                            className="absolute inset-0 w-full h-full object-cover"
                          />
                        ) : (
                          <div className="text-center p-6 space-y-2 text-slate-400">
                            <Camera className="w-12 h-12 mx-auto stroke-1" />
                            <p className="text-sm font-medium text-slate-300">Setting up store camera...</p>
                          </div>
                        )}
                        
                        {/* Overlay controls when streaming */}
                        {stream && (
                          <div className="absolute bottom-4 left-0 right-0 flex justify-center items-center space-x-4 px-4">
                            <button
                              onClick={switchCamera}
                              type="button"
                              className="p-2.5 bg-slate-800/80 backdrop-blur-md text-white rounded-full hover:bg-slate-700 transition"
                              title="Switch Camera Orientation"
                            >
                              <RefreshCw className="w-5 h-5" />
                            </button>
                            <button
                              onClick={capturePhoto}
                              type="button"
                              className="w-14 h-14 bg-orange-500 text-white rounded-full flex items-center justify-center shadow-lg hover:bg-orange-600 transition active:scale-95 border-4 border-white"
                              title="Capture Appraisal Image"
                            >
                              <span className="w-4 h-4 bg-white rounded-full"></span>
                            </button>
                          </div>
                        )}
                      </div>
                    ) : (
                      <div className="relative aspect-video w-full bg-slate-100 rounded-xl overflow-hidden shadow-md">
                        <img 
                          src={capturedImage} 
                          alt="Captured toy analysis reference" 
                          className="w-full h-full object-cover"
                        />
                        <button
                          onClick={clearPhoto}
                          className="absolute top-3 right-3 p-1.5 bg-slate-900/80 text-white rounded-full hover:bg-slate-800 transition"
                        >
                          <X className="w-4 h-4" />
                        </button>
                      </div>
                    )}

                    {/* File Upload Trigger */}
                    <div className="flex items-center justify-between space-x-4">
                      <label className="flex-1 flex items-center justify-center space-x-2 px-4 py-3 border border-slate-300 rounded-xl cursor-pointer hover:bg-slate-50 transition text-sm font-semibold text-slate-700">
                        <Upload className="w-4 h-4 text-orange-500" />
                        <span>Upload Custom Photo</span>
                        <input
                          type="file"
                          accept="image/*"
                          onChange={handleFileUpload}
                          className="hidden"
                        />
                      </label>
                      
                      {capturedImage && (
                        <button
                          onClick={() => runEvaluation(false)}
                          disabled={loading}
                          className="flex-[1.5] flex items-center justify-center space-x-2 bg-orange-500 hover:bg-orange-600 text-white font-bold py-3 px-6 rounded-xl shadow-lg transition disabled:opacity-50 active:scale-95"
                        >
                          {loading ? (
                            <>
                              <RefreshCw className="w-4 h-4 animate-spin" />
                              <span>Evaluating Toy...</span>
                            </>
                          ) : (
                            <>
                              <Sparkles className="w-4 h-4" />
                              <span>Appraise Photo</span>
                            </>
                          )}
                        </button>
                      )}
                    </div>
                  </div>
                )}

                {/* Tab: Manual Search */}
                {activeTab === "search" && (
                  <div className="space-y-4">
                    <div className="space-y-2">
                      <label className="block text-xs font-bold text-slate-500 uppercase tracking-wider">Toy Description or Brand Name</label>
                      <div className="relative">
                        <input
                          type="text"
                          value={searchQuery}
                          onChange={(e) => setSearchQuery(e.target.value)}
                          placeholder="e.g. Vintage 1995 Toy Story Buzz Lightyear Action Figure"
                          className="w-full pl-10 pr-4 py-3 bg-slate-50 border border-slate-300 rounded-xl focus:ring-2 focus:ring-orange-400 focus:border-orange-400 outline-none text-slate-800 transition"
                        />
                        <Search className="w-5 h-5 text-slate-400 absolute left-3 top-3.5" />
                      </div>
                    </div>

                    <button
                      onClick={() => runEvaluation(true)}
                      disabled={loading || !searchQuery.trim()}
                      className="w-full flex items-center justify-center space-x-2 bg-orange-500 hover:bg-orange-600 text-white font-bold py-3 px-6 rounded-xl shadow-lg transition disabled:opacity-50 active:scale-95"
                    >
                      {loading ? (
                        <>
                          <RefreshCw className="w-4 h-4 animate-spin" />
                          <span>Searching Secondary Markets...</span>
                        </>
                      ) : (
                        <>
                          <Sparkles className="w-4 h-4" />
                          <span>Run AI Valuation</span>
                        </>
                      )}
                    </button>
                  </div>
                )}
              </div>
            </div>

            {/* General Help & Error Box */}
            {error && (
              <div className="bg-rose-50 border border-rose-100 rounded-xl p-4 flex items-start space-x-3 text-rose-800">
                <AlertCircle className="w-5 h-5 text-rose-500 shrink-0 mt-0.5" />
                <div className="text-sm">
                  <span className="font-bold">Evaluation issue: </span>
                  {error}
                </div>
              </div>
            )}

            {/* Quick tips card */}
            <div className="bg-slate-100 rounded-2xl p-5 border border-slate-200">
              <h3 className="text-sm font-bold text-slate-700 flex items-center space-x-2">
                <Info className="w-4 h-4 text-orange-500" />
                <span>Tips for accurate picture appraisals:</span>
              </h3>
              <ul className="mt-3 space-y-2 text-xs text-slate-600 list-disc list-inside">
                <li>Place the toy on a plain solid color surface under bright lighting.</li>
                <li>Make sure any visible manufacturer logos or dates are clearly framed.</li>
                <li>Ensure accessories/packaging are included in the view to estimate completeness.</li>
                <li>If the toy is boxed, include images displaying box corner condition.</li>
              </ul>
            </div>
          </div>

          {/* Right Column: AI Insights & Interactive Calculator */}
          <div className="lg:col-span-7 space-y-6">
            
            {!evaluation && !loading && (
              <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-12 text-center flex flex-col items-center justify-center space-y-4">
                <div className="w-16 h-16 bg-orange-50 text-orange-500 rounded-2xl flex items-center justify-center">
                  <Camera className="w-8 h-8 stroke-1.5" />
                </div>
                <div className="max-w-md">
                  <h3 className="text-lg font-bold text-slate-800">Ready for Toy Appraisal</h3>
                  <p className="text-sm text-slate-500 mt-2">
                    Take a clear, direct photograph of the toy or search its item model to run a consignment evaluation report with pricing breakdowns.
                  </p>
                </div>
              </div>
            )}

            {loading && (
              <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-12 text-center flex flex-col items-center justify-center space-y-6">
                <div className="relative">
                  <div className="w-16 h-16 border-4 border-orange-500/20 border-t-orange-500 rounded-full animate-spin"></div>
                  <Sparkles className="w-6 h-6 text-orange-500 absolute inset-0 m-auto animate-bounce" />
                </div>
                <div className="space-y-2">
                  <h3 className="text-lg font-bold text-slate-800">Analyzing Item Market Metrics</h3>
                  <p className="text-sm text-slate-400">Comparing item data points with live eBay listings & retail database guidelines...</p>
                </div>
              </div>
            )}

            {evaluation && !loading && (
              <div className="space-y-6 animate-fadeIn">
                
                {/* Result Block */}
                <div className="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                  <div className="bg-gradient-to-r from-slate-900 to-slate-800 px-6 py-4 text-white flex items-center justify-between">
                    <div>
                      <span className="text-xs font-bold text-orange-400 tracking-wider uppercase">{evaluation.brand}</span>
                      <h2 className="text-lg font-bold leading-tight">{evaluation.toyName}</h2>
                    </div>
                    <div className="text-right">
                      <span className="inline-block px-2.5 py-1 text-xs font-bold rounded-full bg-orange-500/25 border border-orange-400/30 text-orange-300">
                        Demand: {evaluation.demand}
                      </span>
                      <p className="text-xs text-slate-400 mt-1">Est. Year: {evaluation.estimatedYear || "N/A"}</p>
                    </div>
                  </div>

                  {/* Pricing metrics columns */}
                  <div className="grid grid-cols-1 md:grid-cols-2 border-b border-slate-100">
                    
                    {/* Brand New (MSRP) */}
                    <div className="p-6 border-b md:border-b-0 md:border-r border-slate-100 space-y-2">
                      <div className="flex items-center justify-between text-slate-400">
                        <span className="text-xs font-bold uppercase tracking-wider">Estimated Price (New)</span>
                        <Tag className="w-4 h-4 text-slate-300" />
                      </div>
                      <div className="flex items-baseline space-x-1">
                        <span className="text-3xl font-black text-slate-800">${evaluation.priceNew?.toFixed(2) || "0.00"}</span>
                        <span className="text-xs text-slate-500 font-medium">Original Retail</span>
                      </div>
                      <p className="text-xs text-slate-500">Benchmark retail/MSRP when original launched or current box reissue price.</p>
                    </div>

                    {/* Used Resale Avg */}
                    <div className="p-6 space-y-2 bg-orange-50/10">
                      <div className="flex items-center justify-between text-slate-400">
                        <span className="text-xs font-bold uppercase tracking-wider text-orange-700">Used Resale Average</span>
                        <TrendingUp className="w-4 h-4 text-orange-500" />
                      </div>
                      <div className="flex items-baseline space-x-1">
                        <span className="text-3xl font-black text-orange-600">${evaluation.priceUsedAvg?.toFixed(2) || "0.00"}</span>
                        <span className="text-xs text-orange-700 font-bold">eBay / Secondary</span>
                      </div>
                      <div className="flex items-center justify-between text-xs text-slate-500">
                        <span>Range: ${evaluation.priceUsedMin?.toFixed(2) || "0.00"} - ${evaluation.priceUsedMax?.toFixed(2) || "0.00"}</span>
                        <span className="text-slate-400">Conf: {evaluation.confidenceScore || 85}%</span>
                      </div>
                    </div>
                  </div>

                  {/* Valuation Notes */}
                  {evaluation.notes && (
                    <div className="p-5 bg-slate-50 text-slate-600 text-xs border-b border-slate-100 leading-relaxed">
                      <strong className="text-slate-700 font-bold block mb-1">Expert Inspection & Appraiser Notes:</strong>
                      {evaluation.notes}
                    </div>
                  )}

                  {/* Calculator Workspace */}
                  <div className="p-6 space-y-6">
                    <h3 className="text-sm font-black text-slate-800 uppercase tracking-wider flex items-center gap-1.5 border-b border-slate-100 pb-2">
                      <Scale className="w-4 h-4 text-orange-500" />
                      <span>Consignment Profit Calculator</span>
                    </h3>

                    <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                      
                      {/* Left: Interactive Controls */}
                      <div className="space-y-4">
                        <div>
                          <label className="block text-xs font-bold text-slate-500 uppercase tracking-wider mb-1">Target Sale listing Price ($)</label>
                          <div className="relative">
                            <span className="absolute left-3 top-2.5 text-slate-400 font-bold">$</span>
                            <input
                              type="number"
                              value={listingPrice}
                              onChange={(e) => setListingPrice(Number(e.target.value))}
                              className="w-full bg-slate-50 border border-slate-300 rounded-lg pl-7 pr-3 py-2 text-sm font-bold text-slate-800 focus:outline-none focus:ring-2 focus:ring-orange-500"
                            />
                          </div>
                          <p className="text-[10px] text-slate-400 mt-1">Suggested listing defaulted to the average used secondary market price.</p>
                        </div>

                        {/* Splitting Slider */}
                        <div>
                          <div className="flex items-center justify-between mb-1">
                            <label className="text-xs font-bold text-slate-500 uppercase tracking-wider">Store Split: {storeSplit}%</label>
                            <label className="text-xs font-bold text-orange-600 uppercase tracking-wider">Consignor: {consignorSplit}%</label>
                          </div>
                          <input
                            type="range"
                            min="0"
                            max="100"
                            value={storeSplit}
                            onChange={(e) => handleSplitChange(e.target.value, 'store')}
                            className="w-full accent-orange-500 cursor-pointer"
                          />
                          <div className="flex justify-between text-[9px] text-slate-400 mt-1">
                            <span>0% (All to Consignor)</span>
                            <span>Store Standard (40/60)</span>
                            <span>100% (Store buyout)</span>
                          </div>
                        </div>

                        {/* Flat Fees Addons */}
                        <div className="grid grid-cols-2 gap-3">
                          <div>
                            <label className="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1">Cleaning/Prep Fee</label>
                            <div className="relative">
                              <span className="absolute left-2 top-2 text-slate-400 text-xs">$</span>
                              <input
                                type="number"
                                value={cleaningFee}
                                onChange={(e) => setCleaningFee(Number(e.target.value))}
                                className="w-full bg-slate-50 border border-slate-200 rounded-lg pl-5 pr-2 py-1.5 text-xs font-semibold focus:outline-none"
                              />
                            </div>
                          </div>
                          <div>
                            <label className="block text-[10px] font-bold text-slate-500 uppercase tracking-wider mb-1">Consignment Intake Fee</label>
                            <div className="relative">
                              <span className="absolute left-2 top-2 text-slate-400 text-xs">$</span>
                              <input
                                type="number"
                                value={processingFee}
                                onChange={(e) => setProcessingFee(Number(e.target.value))}
                                className="w-full bg-slate-50 border border-slate-200 rounded-lg pl-5 pr-2 py-1.5 text-xs font-semibold focus:outline-none"
                              />
                            </div>
                          </div>
                        </div>
                      </div>

                      {/* Right: Real-time Live Calculations */}
                      <div className="bg-slate-50 rounded-xl p-5 border border-slate-100 flex flex-col justify-between">
                        <div className="space-y-3">
                          <span className="block text-center text-[10px] font-bold text-slate-400 uppercase tracking-wider">Estimated Revenue Split</span>
                          
                          {/* Store Cut Detail */}
                          <div className="flex justify-between items-center border-b border-slate-200/60 pb-2">
                            <div>
                              <span className="text-xs font-semibold text-slate-600 block">Store Share ({storeSplit}%)</span>
                              {financialMetrics.fees > 0 && <span className="text-[10px] text-emerald-600">+ Fees Reimbursements</span>}
                            </div>
                            <span className="text-base font-black text-slate-800">${financialMetrics.storeNetProfit}</span>
                          </div>

                          {/* Consignor Cut Detail */}
                          <div className="flex justify-between items-center border-b border-slate-200/60 pb-2">
                            <div>
                              <span className="text-xs font-semibold text-slate-600 block">Consignor Payout ({consignorSplit}%)</span>
                              {financialMetrics.fees > 0 && <span className="text-[10px] text-rose-500">- Fees Deductions</span>}
                            </div>
                            <span className="text-base font-black text-orange-600">${financialMetrics.consignorNet}</span>
                          </div>

                          <div className="flex justify-between items-center pt-1">
                            <span className="text-xs font-bold text-slate-400">Gross Sale listing Value</span>
                            <span className="text-sm font-bold text-slate-700">${financialMetrics.grossSale.toFixed(2)}</span>
                          </div>
                        </div>

                        {/* Quick info tag on split viability */}
                        <div className="mt-4 p-2 bg-white rounded border border-slate-200 text-[10px] text-slate-500 flex items-center space-x-1.5">
                          <CheckCircle className="w-3.5 h-3.5 text-emerald-500 shrink-0" />
                          <span>Calculated split matches Buddy's Retailers guidelines.</span>
                        </div>
                      </div>
                    </div>

                    {/* Intake Form (Consignor details metadata to save to ledger) */}
                    <div className="border-t border-slate-100 pt-5 space-y-4">
                      <span className="block text-xs font-bold text-slate-500 uppercase tracking-wider">Active Inventory Intake Details</span>
                      <div className="grid grid-cols-1 md:grid-cols-3 gap-3">
                        <div>
                          <label className="block text-[10px] font-semibold text-slate-500 mb-1">Consignor Partner Name</label>
                          <input
                            type="text"
                            value={consignorName}
                            onChange={(e) => setConsignorName(e.target.value)}
                            placeholder="e.g. Sarah Jenkins"
                            className="w-full bg-slate-50 border border-slate-200 rounded-lg px-3 py-1.5 text-xs focus:outline-none"
                          />
                        </div>
                        <div>
                          <label className="block text-[10px] font-semibold text-slate-500 mb-1">Toy Physical Condition</label>
                          <select
                            value={itemCondition}
                            onChange={(e) => setItemCondition(e.target.value)}
                            className="w-full bg-slate-50 border border-slate-200 rounded-lg px-2 py-1.5 text-xs focus:outline-none"
                          >
                            <option value="New In Box (NIB)">New In Box (NIB)</option>
                            <option value="Excellent / Complete">Excellent / Complete</option>
                            <option value="Very Good">Very Good</option>
                            <option value="Good (Play Worn)">Good (Play Worn)</option>
                            <option value="Fair (Minor Damage / Incomplete)">Fair (Minor Damage / Incomplete)</option>
                          </select>
                        </div>
                        <div className="flex items-end">
                          <button
                            onClick={addToLedger}
                            className="w-full bg-slate-900 hover:bg-slate-800 text-white font-bold py-2 px-4 rounded-lg text-xs flex items-center justify-center space-x-1.5 shadow transition"
                          >
                            <Plus className="w-3.5 h-3.5" />
                            <span>Add Item to Store Ledger</span>
                          </button>
                        </div>
                      </div>
                    </div>

                  </div>
                </div>

              </div>
            )}

          </div>
        </div>

        {/* Section: Session Consignment Ledger (Intake inventory dashboard) */}
        <div className="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
          <div className="p-6 border-b border-slate-100 flex flex-col md:flex-row md:items-center md:justify-between gap-4">
            <div>
              <h2 className="text-lg font-bold text-slate-800 flex items-center gap-1.5">
                <FileText className="w-5 h-5 text-orange-500" />
                <span>Buddy's Consignment Session Inventory Ledger</span>
              </h2>
              <p className="text-xs text-slate-400 mt-1">Keep track of evaluated items before drafting contracts, export CSVs, or print intake receipts.</p>
            </div>

            <div className="flex flex-wrap items-center gap-2">
              <select
                value={filterStatus}
                onChange={(e) => setFilterStatus(e.target.value)}
                className="bg-slate-50 border border-slate-200 rounded-lg px-3 py-1.5 text-xs font-semibold text-slate-600 outline-none"
              >
                <option value="all">Show All Drafts</option>
                <option value="active draft">Active Drafts Only</option>
                <option value="contract approved">Approved Agreements</option>
                <option value="declined">Declined Entries</option>
              </select>

              <button
                onClick={exportLedgerToCSV}
                disabled={ledger.length === 0}
                className="flex items-center space-x-1 px-3 py-1.5 rounded-lg border border-slate-200 hover:bg-slate-50 text-slate-600 text-xs font-semibold transition disabled:opacity-50"
              >
                <Printer className="w-3.5 h-3.5" />
                <span>Export Ledger CSV</span>
              </button>

              <button
                onClick={() => setLedger([])}
                disabled={ledger.length === 0}
                className="flex items-center space-x-1 px-3 py-1.5 rounded-lg border border-red-200 hover:bg-red-50 text-red-600 text-xs font-semibold transition disabled:opacity-50"
              >
                <Trash2 className="w-3.5 h-3.5" />
                <span>Clear Session</span>
              </button>
            </div>
          </div>

          {ledger.length === 0 ? (
            <div className="p-12 text-center text-slate-400 space-y-2">
              <FileText className="w-10 h-10 mx-auto stroke-1 text-slate-300" />
              <p className="text-sm font-semibold">Consignment list is currently empty.</p>
              <p className="text-xs max-w-sm mx-auto">Analyze a toy above, select your profit split percentages, and hit 'Add Item to Store Ledger' to begin building today's contract docket.</p>
            </div>
          ) : (
            <div className="overflow-x-auto">
              <table className="w-full text-left border-collapse">
                <thead>
                  <tr className="bg-slate-50 border-b border-slate-100 text-[10px] font-bold uppercase text-slate-400 tracking-wider">
                    <th className="py-4 px-6">Image</th>
                    <th className="py-4 px-6">Date / Consignor</th>
                    <th className="py-4 px-6">Toy Details</th>
                    <th className="py-4 px-6">Evaluation Details</th>
                    <th className="py-4 px-6">Agreed List Price / Split</th>
                    <th className="py-4 px-6">Final Net Split Payout</th>
                    <th className="py-4 px-6 text-center">Contract Status</th>
                    <th className="py-4 px-6 text-right">Actions</th>
                  </tr>
                </thead>
                <tbody className="divide-y divide-slate-100 text-xs text-slate-600">
                  {filteredLedger.map((item) => (
                    <tr key={item.id} className="hover:bg-slate-50/50 transition">
                      <td className="py-4 px-6">
                        {item.image ? (
                          <img src={item.image} alt={item.toyName} className="w-12 h-12 object-cover rounded-lg border border-slate-200" />
                        ) : (
                          <div className="w-12 h-12 bg-slate-100 rounded-lg flex items-center justify-center text-slate-400 font-bold">
                            N/A
                          </div>
                        )}
                      </td>
                      <td className="py-4 px-6">
                        <span className="font-semibold text-slate-800 block">{item.consignor}</span>
                        <span className="text-[10px] text-slate-400 flex items-center gap-1">
                          <Clock className="w-3 h-3" />
                          {item.date}
                        </span>
                      </td>
                      <td className="py-4 px-6">
                        <span className="font-bold text-slate-900 block">{item.toyName}</span>
                        <span className="text-[10px] text-orange-600 font-bold uppercase">{item.brand}</span>
                      </td>
                      <td className="py-4 px-6 space-y-1">
                        <div className="flex items-center space-x-1.5 text-slate-500">
                          <span className="font-semibold text-[10px]">MSRP:</span>
                          <span>${item.suggestedRetail?.toFixed(2) || "0.00"}</span>
                        </div>
                        <div className="flex items-center space-x-1.5 text-slate-500">
                          <span className="font-semibold text-[10px] text-orange-600">Est. Used:</span>
                          <span className="font-bold text-slate-700">${item.marketAverage?.toFixed(2) || "0.00"}</span>
                        </div>
                        <span className="inline-block px-1.5 py-0.5 bg-slate-100 border border-slate-200 text-[10px] font-medium text-slate-600 rounded">
                          Cond: {item.condition}
                        </span>
                      </td>
                      <td className="py-4 px-6 space-y-1">
                        <span className="text-sm font-black text-slate-800">${item.agreedListingPrice?.toFixed(2)}</span>
                        <span className="block text-[10px] text-slate-400">Split: {item.storeSplit}% S / {item.consignorSplit}% C</span>
                      </td>
                      <td className="py-4 px-6 space-y-1">
                        <div className="flex items-center justify-between gap-2 max-w-[120px]">
                          <span className="text-[10px] font-semibold text-slate-400">Consignor:</span>
                          <span className="font-bold text-orange-600">${item.consignorPayout.toFixed(2)}</span>
                        </div>
                        <div className="flex items-center justify-between gap-2 max-w-[120px]">
                          <span className="text-[10px] font-semibold text-slate-400">Store:</span>
                          <span className="font-bold text-slate-800">${item.storeProfit.toFixed(2)}</span>
                        </div>
                      </td>
                      <td className="py-4 px-6 text-center">
                        <select
                          value={item.status}
                          onChange={(e) => updateLedgerStatus(item.id, e.target.value)}
                          className={`px-2 py-1 rounded text-[10px] font-bold border outline-none ${
                            item.status === "Contract Approved"
                              ? "bg-emerald-50 border-emerald-200 text-emerald-700"
                              : item.status === "Declined"
                              ? "bg-rose-50 border-rose-200 text-rose-700"
                              : "bg-orange-50 border-orange-200 text-orange-700"
                          }`}
                        >
                          <option value="Active Draft">Active Draft</option>
                          <option value="Contract Approved">Contract Approved</option>
                          <option value="Declined">Declined</option>
                        </select>
                      </td>
                      <td className="py-4 px-6 text-right">
                        <button
                          onClick={() => deleteLedgerItem(item.id)}
                          className="p-1.5 text-slate-400 hover:text-red-500 rounded-lg hover:bg-red-50 transition"
                          title="Delete Intake Record"
                        >
                          <Trash2 className="w-4 h-4" />
                        </button>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          )}
        </div>

      </main>

      {/* Guide/Strategy Modal */}
      {showGuide && (
        <div className="fixed inset-0 z-50 overflow-y-auto flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm animate-fadeIn">
          <div className="bg-white rounded-2xl max-w-2xl w-full p-6 sm:p-8 space-y-6 shadow-2xl relative">
            <button
              onClick={() => setShowGuide(false)}
              className="absolute top-4 right-4 p-1.5 text-slate-400 hover:text-slate-600 rounded-full hover:bg-slate-100 transition"
            >
              <X className="w-5 h-5" />
            </button>

            <div className="flex items-center space-x-3">
              <div className="p-2 bg-orange-50 text-orange-500 rounded-xl">
                <Scale className="w-6 h-6" />
              </div>
              <h2 className="text-xl font-bold text-slate-900">Buddy's Consignment Best Practices</h2>
            </div>

            <div className="space-y-4 text-sm text-slate-600 leading-relaxed">
              <p>
                Consignment sales are a zero-inventory-cost way to stock unique, hard-to-find vintage or modern high-demand toys. Use this app to build consistency and trust during walk-in evaluations.
              </p>

              <div className="space-y-2">
                <h3 className="font-bold text-slate-800">1. Agreeing on Listing Prices</h3>
                <p>
                  Used toys often sell for around <strong>35% - 60%</strong> of original MSRP unless they are highly rare collector items (which sell at premiums). Our AI appraisal checks current secondary markets to give you the realistic average resale price.
                </p>
              </div>

              <div className="space-y-2">
                <h3 className="font-bold text-slate-800">2. Designing the Split Structure</h3>
                <p>
                  A standard split ratio for physical toy stores is <strong>40% to the store, and 60% to the consignor</strong>. If the toy requires deep washing or specialized accessory replacements, add custom cleaning or intake fees to ensure your store's labor margins remain healthy.
                </p>
              </div>

              <div className="space-y-2">
                <h3 className="font-bold text-slate-800">3. Setting Status Controls</h3>
                <p>
                  Use the <strong>Consignment Session Ledger</strong> at the bottom of the workspace to queue up multiple items presented by a single consignor. Once they sign your consignment contract, update their status to "Contract Approved" and print or export the checklist as a receipt for their records!
                </p>
              </div>
            </div>

            <div className="pt-4 border-t border-slate-100 flex justify-end">
              <button
                onClick={() => setShowGuide(false)}
                className="bg-orange-500 hover:bg-orange-600 text-white font-bold px-6 py-2 rounded-xl text-sm shadow transition"
              >
                Got It, Thanks!
              </button>
            </div>
          </div>
        </div>
      )}

      {/* API Key Modal Setup */}
      {showKeyModal && (
        <div className="fixed inset-0 z-50 overflow-y-auto flex items-center justify-center p-4 bg-slate-900/60 backdrop-blur-sm animate-fadeIn">
          <div className="bg-white rounded-2xl max-w-md w-full p-6 shadow-2xl space-y-6 relative">
            <button
              onClick={() => setShowKeyModal(false)}
              className="absolute top-4 right-4 p-1.5 text-slate-400 hover:text-slate-600 rounded-full hover:bg-slate-100 transition"
            >
              <X className="w-5 h-5" />
            </button>

            <div className="flex items-center space-x-3">
              <div className="p-2 bg-orange-50 text-orange-500 rounded-xl">
                <Settings className="w-5 h-5" />
              </div>
              <h2 className="text-lg font-bold text-slate-900">Custom Gemini API Key Setup</h2>
            </div>

            <div className="space-y-3 text-xs text-slate-500 leading-relaxed">
              <p>
                By default, this application executes via standard secure Sandbox environment headers. To bypass global sandbox usage quotas, paste your dedicated Google Gemini API key.
              </p>
              <p>Your keys are used exclusively for locally outbound browser requests directly to Google API servers.</p>
            </div>

            <div className="space-y-2">
              <label className="block text-xs font-bold text-slate-500 uppercase tracking-wider">Gemini API Key</label>
              <input
                type="password"
                value={apiKey}
                onChange={(e) => setApiKey(e.target.value)}
                placeholder="AIzaSy..."
                className="w-full bg-slate-50 border border-slate-300 rounded-lg px-3 py-2 text-sm outline-none focus:ring-2 focus:ring-orange-500 focus:border-orange-500 transition"
              />
            </div>

            <div className="pt-4 border-t border-slate-100 flex items-center justify-between">
              <button
                onClick={() => setApiKey("")}
                className="text-red-500 hover:text-red-600 text-xs font-bold"
              >
                Clear Custom Key
              </button>
              <button
                onClick={() => setShowKeyModal(false)}
                className="bg-slate-900 hover:bg-slate-800 text-white font-bold px-6 py-2 rounded-xl text-sm shadow transition"
              >
                Save & Close
              </button>
            </div>
          </div>
        </div>
      )}

      {/* Premium Footer */}
      <footer className="bg-white border-t border-slate-200 py-6 mt-12">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4">
          <p className="text-xs text-slate-400">
            &copy; {new Date().getFullYear()} Buddy's Toys and Collectibles. Handcrafted for modern boutique toy retailers.
          </p>
          <div className="flex items-center space-x-4 text-xs text-slate-400">
            <span>Powered by Gemini 2.5 Flash</span>
            <span className="w-1.5 h-1.5 bg-emerald-500 rounded-full"></span>
            <span>Real-time Secondary Market Analytics Enabled</span>
          </div>
        </div>
      </footer>
    </div>
  );
}
