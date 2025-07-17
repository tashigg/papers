# Tashi Tokenomics - Complete System Overview

## **Executive Summary**

Tashi implements a sophisticated DePIN tokenomics model that bridges traditional SaaS economics (USD payments) with crypto incentives (token rewards). The system uses **failure-tolerant reputation mechanisms**, **multi-factor node selection**, and **geographic optimization** to create a fair, sustainable, and high-performance edge compute network.

**Key Innovation**: Separation of market consequences (reputation) from financial consequences (slashing) enables infrastructure-tolerant yet quality-focused network governance.

---

## **1. Revenue & Economic Foundation**

### **Core Revenue Model**
```
Developer Payment: USD → Credits (1:1) → Service Consumption
Network Revenue: $0.05 per Daily Concurrent User (CCU)
Revenue Backing: 1:1 USD backing for all reward points
Tax Treatment: Reward Points remain non-taxable until converted
```

### **Tiered CCU Pricing Structure**
| Volume Tier | Price/CCU | Example Monthly Cost |
|-------------|-----------|---------------------|
| **0-10K CCUs** | $0.05 | $15,000 |
| **10K-100K CCUs** | $0.04 | $120,000 |
| **100K-1M CCUs** | $0.03 | $900,000 |
| **1M+ CCUs** | $0.02 | $600,000/1M CCUs |

**Enterprise Impact**: Fortnite-scale (10M CCUs) pays $211K/day vs $500K flat rate (58% savings)

### **Revenue Distribution Model**
```
Daily Revenue ($50K example):
├─ Treasury (30%): $15,000
│  ├─ Stripe Fees: $1,750
│  ├─ Infrastructure: $500  
│  ├─ Buyback Buffer: $3,000
│  ├─ Conduit Reserve: $5,000
│  └─ Foundation Net: $4,750
├─ Orchestrators (10%): $5,000
└─ Resources (60%): $30,000
   ├─ Availability (10%): $3,000
   ├─ Completion (30%): $9,000
   └─ Incentives (60%): $18,000
```

---

## **2. Three-Tier Network Architecture**

### **Tier 1: TASHI Stakers**
```python
role = {
    'function': 'Provide capital to secure network operations',
    'mechanism': 'Delegate stake to Node Licensees via stake pools',
    'rewards': 'Share of staking rewards from delegated licensees',
    'governance': 'Vote on economic parameters (40% quorum, 66% threshold)',
    'risk': 'Slashing for poor performance of delegated licensees'
}
```

### **Tier 2: Node Licensees**
```python
role = {
    'function': 'Business entities operating network infrastructure',
    'examples': ['Game publishers (Blizzard)', 'Infrastructure providers'],
    'requirements': 'Stake delegation to activate nodes',
    'rewards': 'Completion rewards + availability rewards + reputation building',
    'responsibilities': 'Select and manage Node Operators, bear reputation risk'
}
```

### **Tier 3: Node Operators**
```python
role = {
    'function': 'Run actual compute, bandwidth, and consensus infrastructure',
    'examples': ['Game players', 'Dedicated servers', 'Edge devices'],
    'requirements': 'Meet technical specs, maintain connectivity',
    'rewards': 'Share of licensee rewards based on performance',
    'stake': 'No direct staking requirement (risk borne by licensees)'
}
```

---

## **3. Tiered Staking Economics**

### **Enterprise-Friendly Staking Structure**
```python
def calculate_staking_cost(node_count):
    """Tiered staking reduces enterprise barriers"""
    tiers = [
        (1_000, 10),      # First 1K nodes: $10/node
        (10_000, 8),      # Next 9K nodes: $8/node
        (100_000, 6),     # Next 90K nodes: $6/node  
        (∞, 4)            # Additional nodes: $4/node
    ]
    
    # Example: 1M nodes = $4.2M (vs $10M flat rate)
    # Savings: 58% cost reduction for large deployments
```

### **Stake Pool Architecture**
```
Foundation Pool (30%): Emergency allocation, market stabilization
Community Pools (50%): Multiple competing pools with different strategies
Enterprise Pools (20%): Direct control for large operators (Blizzard, etc.)
```

### **Co-Staking Mechanics**
- **Delegator**: 50% of stake rewards + slashing protection
- **Licensee**: 50% of stake rewards + 100% of job rewards + reputation risk
- **Risk Sharing**: Both parties subject to slashing for poor performance

---

## **4. Dual Penalty System**

### **Reputation Reduction (Market Mechanism)**
```python
# Threshold: 15% failure rate  
# Purpose: Job selection probability (market signal)
# Recovery: Possible through consistent good performance

def calculate_reputation_penalty(failure_rate, pattern_suspiciousness):
    if failure_rate <= 0.15:  # 15% tolerance
        return 0  # No penalty within normal variance
    
    excess_rate = failure_rate - 0.15
    base_impact = excess_rate * 2.0  # 2x multiplier for market responsiveness
    pattern_multiplier = 1 + (pattern_suspiciousness * 0.5)  # Max 1.5x
    
    return min(0.15, base_impact * pattern_multiplier)  # Cap at 0.15 loss
```

### **Stake Slashing (Financial Protection)**
```python
# Threshold: 35% failure rate + reputation < 1.0 (double-gated)
# Purpose: Financial penalty for persistent poor behavior
# Recovery: Automatic when reputation recovers above 1.0

def calculate_stake_slashing(failure_rate, reputation, pattern_suspiciousness):
    # Gate 1: Must exceed high failure rate threshold
    if failure_rate <= 0.35:
        return 0
    
    # Gate 2: Must have damaged reputation
    if reputation >= 1.0:
        return 0  # Reputation protection
    
    # Calculate financial penalty
    excess_rate = failure_rate - 0.35
    severity_multiplier = excess_rate / 0.35
    pattern_multiplier = 1 + (pattern_suspiciousness * 2.0)  # Up to 3x
    reputation_multiplier = 1.0 - reputation
    
    return severity_multiplier * pattern_multiplier * reputation_multiplier * base_damage_cost
```

### **Infrastructure Protection Examples**
| Scenario | Reputation Impact | Financial Impact |
|----------|------------------|------------------|
| **Power Outage** (20% failures, clustered) | -0.105 (job reduction) | $0.00 |
| **ISP Issues** (25% failures, sporadic) | -0.150 (moderate reduction) | $0.00 |
| **Gaming Behavior** (40% failures, suspicious) | -0.150 + escalation | $0.007+ |

---

## **5. Failure-Tolerant Reputation System**

### **Pattern-Based Assessment**
```python
failure_patterns = {
    'clustered_outage': {
        'suspiciousness': 0.1,    # 10% suspicious (likely legitimate)
        'examples': 'Power outages, ISP failures'
    },
    'normal_sporadic': {
        'suspiciousness': 0.2,    # 20% suspicious (normal variance)  
        'examples': 'Random hardware/network issues'
    },
    'too_regular': {
        'suspiciousness': 0.8,    # 80% suspicious (gaming behavior)
        'examples': 'Failures every X hours exactly'
    },
    'rapid_cycling': {
        'suspiciousness': 0.9,    # 90% suspicious (clear gaming)
        'examples': 'On/off within minutes repeatedly'
    }
}
```

### **Grace Period System**
```python
# New node protection (7-day grace period)
grace_tolerance = {
    'day_0': 0.35,    # 35% failure tolerance
    'day_3': 0.275,   # Gradual reduction
    'day_7': 0.20     # Standard tolerance
}

# Penalty reduction during grace period:
# - 50% reduction for reputation penalties
# - 75% reduction for financial penalties
```

---

## **6. Multi-Factor Node Selection**

### **Service-Specific Selection Weights**
| Service | Latency | Reputation | EPGP | Use Case |
|---------|---------|------------|------|----------|
| **Relay** | 50% | 30% | 20% | Real-time gaming sessions |
| **Lobby** | 30% | 40% | 30% | Session handshaking/recovery |
| **Matchmaking** | 20% | 20% | 60% | Short-term peer matching |
| **Analytics** | 10% | 30% | 60% | Background processing |

### **EPGP Fairness System**
```python
# Effort Points / Gear Points mechanism
epgp_priority = effort_points / gear_points

effort_points = (
    availability_hours * 0.1 +     # 0.1 EP per hour available
    completed_jobs * 1.0 +         # 1.0 EP per completed job  
    quality_bonus_points           # Performance bonuses
)

# Job allocation updates:
# Selected: gear_points += job_value
# Weekly decay: gear_points *= 0.9 (prevents hoarding)
```

### **Selection Results by Service Type**
**Relay Service (High Reliability):**
- Veterans: 90% of jobs (performance critical)
- New Nodes: 10% of jobs (limited opportunity)

**Matchmaking Service (Low Reliability):**
- Veterans: 65% of jobs (still competitive)
- New Nodes: 35% of jobs (meaningful participation)

---

## **7. Geographic Optimization & Redundancy**

### **Latency-Based Selection**
```python
def select_nodes_with_redundancy(candidates, job_location, count, service_type):
    # Step 1: Geographic filtering by latency requirements
    eligible = candidates.filter(node => 
        node.latency_to(job_location) <= service.max_latency
    )
    
    # Step 2: Multi-factor scoring
    scored = eligible.map(node => ({
        node: node,
        score: calculate_selection_score(node, service_type)
    }))
    
    # Step 3: Select top N for redundancy
    return scored.sort_by_score().take(count)
}
```

### **Redundancy by Service Type**
- **Relay**: 3-5 nodes (primary + backups for session-critical services)
- **Lobby**: 2-3 nodes (primary + secondary for handshaking)
- **Matchmaking**: 1-2 nodes (primary + optional backup)
- **Analytics**: 1 node (background processing, retryable)

---

## **8. Reward Point & Incentive System**

### **Reward Point Mechanics**
```python
reward_points = {
    'backing': '1:1 USD from network revenue',
    'properties': 'Soulbound (non-transferable)',
    'tax_treatment': 'Non-taxable until conversion',
    'redemption_options': {
        'network_services': '1:1 value + 25% cash back',
        'staking_conversion': '1:1 value + 15% cash back + tax event',
        'direct_conversion': '1:1 value + 0% cash back + tax event'
    }
}
```

### **Incentive Pool Sustainability**
All usage pattern testing shows **sustainable economics**:
- **Balanced Usage** (40% network, 30% staking): 1.72x sustainability ratio
- **High Network Use** (80% network): 1.16x sustainability ratio  
- **High Staking** (50% staking): 2.00x sustainability ratio

### **Dynamic Cash Back Rates**
```python
def calculate_dynamic_rates(treasury_ratio, staked_ratio):
    network_rate = 0.25  # Base 25%
    staking_rate = 0.15  # Base 15%
    
    # Boost network usage when treasury is healthy
    if treasury_ratio > 2.0:
        network_rate = min(0.35, network_rate * 1.2)
    
    # Encourage staking when participation is low
    if staked_ratio < 0.3:
        staking_rate = min(0.25, staking_rate * 1.5)
    
    return network_rate, staking_rate
```

---

## **9. DePIN Security Model**

### **Attack Vector Protection**
Unlike traditional blockchain networks, Tashi faces **service manipulation attacks**:

**Service Denial Attack:**
- **Method**: Large staker refuses allocation to competitive regions
- **Defense**: Minimum regional allocation requirements + slashing

**Quality Degradation Attack:**
- **Method**: Coordinated poor service to competitor games
- **Defense**: SLA enforcement + cross-validation + performance slashing

**Economic Manipulation Attack:**
- **Method**: Artificial scarcity to drive up prices
- **Defense**: Price ceilings + alternative capacity + emergency protocols

### **Multi-Pool Competition**
```python
stake_pools = {
    'foundation_pool': {
        'allocation': '30% of total stake',
        'purpose': 'Emergency allocation, market stabilization'
    },
    'community_pools': {
        'allocation': '50% of total stake', 
        'purpose': 'Multiple competing strategies and SLAs'
    },
    'enterprise_pools': {
        'allocation': '20% of total stake',
        'purpose': 'Direct control for large operators'
    }
}
```

---

## **10. Token Allocation & Governance**

### **Token Distribution (10B Total Supply)**
```
Network Rewards:     35% (3.5B) - 48 months linear distribution
Foundation:          20% (2.0B) - 25% TGE + 48 months linear
Team:                15% (1.5B) - 12 month cliff + 24 months linear
Seed + Community:    20% (2.0B) - Staggered vesting schedules
Advisors + Testnet:  10% (1.0B) - Performance and time-based
```

### **Dual-Track Governance**
```python
governance_tracks = {
    'service_parameters': {
        'voting_token': 'API Credits (usage-based)',
        'scope': 'Service configs, SLA requirements, features',
        'quorum': '10% of outstanding credits',
        'threshold': '50% majority'
    },
    'economic_parameters': {
        'voting_token': 'Staked TASHI (sTASHI)',
        'scope': 'Economic params, protocol upgrades, treasury',
        'quorum': '40% of staked supply', 
        'threshold': '66% supermajority'
    }
}
```

---

## **11. Economic Sustainability Analysis**

### **Break-Even Analysis**
```python
# Daily revenue requirements for sustainability
min_daily_revenue = 2000  # $2K/day minimum
sustainable_daily_revenue = 50000  # $50K/day target

sustainability_metrics = {
    'treasury_growth': '$4,750/day at $50K revenue',
    'operator_incentives': '1.72x coverage ratio',
    'infrastructure_costs': 'Fully covered with growth margin',
    'development_funding': 'Sustainable long-term'
}
```

### **Network Growth Projections**
| Year | Target CCUs | Daily Revenue | Monthly Revenue | Sustainability |
|------|-------------|---------------|-----------------|----------------|
| **Y1** | 1M | $50K | $1.5M | ✅ Sustainable |
| **Y2** | 5M | $150K | $4.5M | ✅ High Growth |
| **Y3** | 20M | $400K | $12M | ✅ Market Leader |

---

## **12. Implementation Roadmap**

### **Phase 1: Core Infrastructure (Months 1-3)**
- ✅ USD payment processing with Stripe integration
- ✅ Reward Point system with redemption mechanisms
- ✅ Basic reputation tracking and dual penalty system
- ✅ Geographic allocation algorithm deployment

### **Phase 2: Advanced Features (Months 4-6)**
- ✅ Multi-pool staking architecture with co-staking
- ✅ EPGP fairness system implementation
- ✅ Insurance pool system for publishers
- ✅ Dynamic cash back rate adjustments

### **Phase 3: Optimization & Enterprise (Months 7-12)**
- ✅ Advanced governance implementation
- ✅ Enterprise integration and partnerships
- ✅ Automated security response systems
- ✅ Economic simulation and stress testing

---

## **13. Key Innovation Summary**

### **Economic Innovations**
1. **USD-Backed Sustainability**: Revenue-first tokenomics eliminates common DePIN sustainability issues
2. **Dual Penalty System**: Separates market consequences from financial consequences
3. **Tiered Staking**: Reduces enterprise barriers while maintaining security
4. **Service-Differentiated Selection**: Reliability where needed, opportunity where appropriate

### **Technical Innovations**
1. **Failure-Tolerant Reputation**: Pattern analysis distinguishes infrastructure issues from gaming
2. **EPGP Fairness**: Prevents monopolization while rewarding performance
3. **Geographic Optimization**: Automatic latency-based selection with redundancy
4. **Multi-Pool Competition**: Market-based allocation prevents single-point control

### **Governance Innovations**
1. **Three-Tier Architecture**: Separates capital, business logic, and operations
2. **Dual-Track Governance**: Users and stakers vote on different aspects
3. **DePIN Security Model**: Focuses on service manipulation rather than consensus attacks
4. **Insurance Pools**: Protects publishers from systematic network failures

---

## **Conclusion**

The Tashi tokenomics model represents a significant advancement in DePIN economics by:

- **Solving Sustainability**: USD-backed revenue creates guaranteed economic foundation
- **Enabling Fairness**: EPGP system provides opportunities for new participants
- **Ensuring Quality**: Reputation system rewards performance while tolerating infrastructure issues
- **Optimizing Performance**: Geographic and redundancy selection maximizes service quality
- **Preventing Gaming**: Multi-layered security prevents service manipulation attacks

**Strategic Impact**: This model could become a **reference implementation** for sustainable DePIN tokenomics, bridging traditional SaaS business models with decentralized infrastructure incentives.

The system successfully balances the **impossible triangle** of DePIN networks: **decentralization**, **performance**, and **sustainability** through innovative economic design rather than technological complexity alone.